<script>
    import Score from './Score.svelte';
    import questions from '../data/questions';
    import { shuffleArray } from '../helpers/helpers';

    let hasReplied = false;
    let hasRepliedBonus = false;
    let bonusReply;
    let activeQuestion = 0;
    let isReplyCorrect;
    let isBonusCorrect;
    let score = 0;
    let shuffledQuestions = [];
    let bonusPropositions = [];

    const checkResponse = (from) => {
        if (hasReplied) return;
        
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
            score++;
            isBonusCorrect = true;
        } else {
            isBonusCorrect = false;
        }
        hasRepliedBonus = true;
    };

    const getRandomAnswers = (type, excluded) => {
        bonusPropositions = questions.filter(question => question.answer === type && question.bonus !== excluded);
        shuffleArray(bonusPropositions);
        bonusPropositions = bonusPropositions.slice(0, 2);
        bonusPropositions.splice(Math.floor(Math.random() * 3), 0, shuffledQuestions[activeQuestion]);
    };

    const nextQuestion = () => {
        hasReplied = false;
        hasRepliedBonus = false
        bonusReply = undefined;
        activeQuestion++;
    };

    const resetQuiz = () => {
        shuffledQuestions = shuffleArray([...questions]);
        activeQuestion = 0;
    };
    resetQuiz();
</script>

<Score score={score} />
<div class="quiz-wrapper">
    {#if activeQuestion === shuffledQuestions.length}
        <div class="quiz-complete">
            <h3>Quiz complete</h3>
            <p>Your final score: {score}/{shuffledQuestions.length}</p>

            <button on:click={resetQuiz}>Start over?</button>
        </div>
    {:else}
        <h2>This picture was taken from...</h2>
        <div class="image-wrapper">
            <img src=/images/{shuffledQuestions[activeQuestion].id+1}.jpg alt="" />
            <div class="buttons-wrapper">
                <button on:click={() => checkResponse('movie')}>🎬 a movie</button>
                <button on:click={() => checkResponse('city')}>🦠 the Coronavirus pandemic</button>
            </div>
        </div>
    {/if}
    {#if hasReplied}
        <div>
            {#if isReplyCorrect}
                <p>Good answer, congratulations ! Do you know from what {shuffledQuestions[activeQuestion].answer} ?</p>
                <ul class="bonus-propositions">
                {#each bonusPropositions as proposition, index}
                    <li>
                        <button
                            class:goodAnswer="{hasRepliedBonus && proposition.bonus === shuffledQuestions[activeQuestion].bonus}"
                            class:badAnswer="{hasRepliedBonus && !isBonusCorrect && bonusReply === proposition.bonus}"
                            class="bonus-answer"
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
            <span class="bonus-reply-feedback">
                {#if isBonusCorrect}
                    Yeah, an extra point for you!
                {:else}
                    Nope !
                {/if}
            </span>
            <button on:click={nextQuestion}>Next question ➔</button>
        </div>
    {/if}
</div>

<style>
    .quiz-wrapper {
        margin: 100px auto;
    }

    @media (min-width: 800px) {
        .quiz-wrapper {
            max-width: 600px;
        }
    }

    h2 {
		color: #fff;
        font-size: 4rem;
        font-weight: 800;
        text-align: center;
        -webkit-text-stroke: 2px #000;
    }

    h3 {
        color: #000;
        font-size: 3rem;
    }
    
    img {
        width: 100%;
        margin: 0 auto;
        border: 4px solid #000;
    }

    .buttons-wrapper {
        margin-top: 10px;
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
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

    .bonus-reply-wrapper {
        display: flex;
        align-items: center;
    }

    .bonus-reply-feedback {
        margin-right: 10px;
        font-size: 2rem;
        font-weight: 700;
    }

    .quiz-complete {
        padding: 20px;
        background: #fff;
        border: 4px solid #000;
    }
</style>