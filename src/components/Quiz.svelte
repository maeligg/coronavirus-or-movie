<script>
    import Index from './Index.svelte';
    import QuizResults from './QuizResults.svelte';
    import questions from '../data/questions';
    import { shuffleArray } from '../helpers/helpers';

    let hasReplied = false;
    let hasRepliedBonus = false;
    let userAnswer = null;
    let bonusReply;
    let activeQuestion = 0;
    let isReplyCorrect;
    let isBonusCorrect;
    let score = 0;
    let scoreBonus = 0;
    let shuffledQuestions = [];
    let bonusPropositions = [];

    const checkResponse = (from) => {
        if (hasReplied) return;
            
        userAnswer = from;
        if (from === shuffledQuestions[activeQuestion].answer) {
            isReplyCorrect = true;
            score++;
            getRandomAnswers(shuffledQuestions[activeQuestion].answer, shuffledQuestions[activeQuestion].bonus);
        } else {
            isReplyCorrect = false;
        }

        hasReplied = true;
        return;
    };

    const checkBonus = (answer) => {
        if (hasRepliedBonus) return;

        bonusReply = answer;
        // If user answered correctly
        if (answer === shuffledQuestions[activeQuestion].bonus) {
            scoreBonus++;
            isBonusCorrect = true;
        } else {
            isBonusCorrect = false;
        }
        hasRepliedBonus = true;
    };

    const getRandomAnswers = (type, excluded) => {
        bonusPropositions = questions.filter(question => question.answer === type && question.bonus !== excluded);
        shuffleArray(bonusPropositions);
        bonusPropositions = bonusPropositions.slice(0, 3);
        bonusPropositions.splice(Math.floor(Math.random() * 4), 0, shuffledQuestions[activeQuestion]);
    };

    const nextQuestion = () => {
        hasReplied = false;
        userAnswer = null;
        hasRepliedBonus = false
        bonusReply = undefined;
        activeQuestion++;
    };

    const resetQuiz = () => {
        shuffledQuestions = shuffleArray([...questions]);
        shuffledQuestions = shuffledQuestions.slice(0, 10);
        activeQuestion = 0;
        score = 0;
        scoreBonus = 0;
    };
    resetQuiz();
</script>

{#if activeQuestion < shuffledQuestions.length}
    <Index current={activeQuestion} amount={shuffledQuestions.length} />
{/if}

{#if activeQuestion === shuffledQuestions.length}
    <QuizResults totalQuestions={shuffledQuestions.length} score={score} scoreBonus={scoreBonus} resetQuiz={resetQuiz} />
{:else}
    <div class="quiz-wrapper">
        <h2>This picture is from...</h2>
        <div class="image-wrapper">
            <img class="image" src=/images/{shuffledQuestions[activeQuestion].id+1}.jpg width="1200" height="667" alt="" />
            <div class="buttons-wrapper">
                <button 
                    class:goodAnswer="{hasReplied && isReplyCorrect && userAnswer === 'city'}"
                    class:badAnswer="{hasReplied && !isReplyCorrect && userAnswer === 'city'}"
                    disabled="{hasReplied}"
                    on:click={() => checkResponse('city')}><img src="images/corona.png" alt="Icon virus">COVID-19</button>
                <button 
                    class:goodAnswer="{hasReplied && isReplyCorrect && userAnswer === 'movie'}"
                    class:badAnswer="{hasReplied && !isReplyCorrect && userAnswer === 'movie'}"
                    disabled="{hasReplied}"
                    on:click={() => checkResponse('movie')}><img src="images/clap.png" alt="Icon movie clapper">MOVIE</button>
            </div>
        </div>
    {#if hasReplied}
        <div>
            {#if isReplyCorrect}
                <p>Good answer, congratulations!<br>Do you know from what {shuffledQuestions[activeQuestion].answer}?</p>
                <ul class="bonus-propositions">
                {#each bonusPropositions as proposition, index}
                    <li>
                        <button
                            class:goodAnswer="{hasRepliedBonus && proposition.bonus === shuffledQuestions[activeQuestion].bonus}"
                            class:badAnswer="{hasRepliedBonus && !isBonusCorrect && bonusReply === proposition.bonus}"
                            class="bonus-answer"
                            disabled="{hasRepliedBonus}"
                            on:click={() => checkBonus(proposition.bonus)}
                        >
                            {proposition.bonus}
                        </button>
                    </li>
                {/each}
                </ul>
            {:else}
                <p>Sorry, incorrect.</p>
                <button on:click={nextQuestion}>Next question ➔</button>
            {/if}
        </div>
    {/if}
    {#if hasRepliedBonus}
        <div class="bonus-reply-wrapper">
            <p class="bonus-reply-feedback">
                {#if isBonusCorrect}
                    Yeah, an extra point for you!
                {:else}
                    Sorry, incorrect.
                {/if}
            </p>
            <button on:click={nextQuestion}>Next question ➔</button>
        </div>
    {/if}
</div>
{/if}

<style>
    .quiz-wrapper {
        margin: 70px auto;
        flex-grow: 1;
    }

    h2 {
		color: #fff;
        font-size: 3.5rem;
        line-height: 1.2;
        font-weight: 800;
        margin-bottom: 20px;
        margin-top: 0;
        text-align: center;
        -webkit-text-stroke: 2px #000;
    }
    
    .image {
        width: 100%;
        height: auto;
        margin: 0 auto;
        border: 3px solid #000;
    }

    .buttons-wrapper {
        margin-top: 10px;
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
        min-width: 200px;
    }

    .buttons-wrapper button {
        min-width: 120px;
    }
    .buttons-wrapper img {
        display: block;
        width: 3rem;
        height: auto;
        margin: 0 auto;
    }

    .bonus-propositions {
        display: flex;
        flex-wrap: wrap;
        padding: 0;
        list-style: none;
    }

    .bonus-answer {
        margin: 0 10px 10px 0;
        line-height: 1.5;
    }

    .goodAnswer {
        background: green;
        color: #fff;
    }

    .badAnswer {
        background: red;
        color: #fff;
    }

    p {
        margin-top: 10px;
        margin-bottom: 10px;    
    }

    .bonus-reply-feedback {
        margin-right: 10px;
        font-size: 2rem;
        font-weight: 700;
    }

    @media (min-width: 750px) {
        .quiz-wrapper {
            margin-top: 100px;
            max-width: 600px;
        }

        h2 {
            margin-bottom: 50px;
            font-size: 4rem;
        }
        .buttons-wrapper img {
            width: 4rem;
        }
        .image {
            border: 4px solid #000;
        }
        .bonus-reply-wrapper {
            display: flex;
            align-items: center;
        }
        p {
            margin-top: 20px;
            margin-bottom: 20px;    
        }
    }
</style>