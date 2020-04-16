<script>
    import Score from './Score.svelte';
    import questions from '../data/questions';
    import { shuffleArray } from '../helpers/helpers';

    let hasReplied = false;
    let hasRepliedBonus = false;
    let activeQuestion = 0;
    let isReplyCorrect;
    let isBonusCorrect;
    let score = 0;
    let shuffledQuestions = [];
    let bonusPropositions = [];

    const checkResponse = (from) => {
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
        bonusPropositions = bonusPropositions.slice(0, 2);
        bonusPropositions.push(shuffledQuestions[activeQuestion]);
        shuffleArray(bonusPropositions);
    };

    const nextQuestion = () => {
        hasReplied = false;
        hasRepliedBonus = false
        activeQuestion++;
    };

    const resetQuiz = () => {
        shuffledQuestions = shuffleArray([...questions]);
        activeQuestion = 0;
    };
    resetQuiz();
</script>

<Score score={score} />
{#if activeQuestion === shuffledQuestions.length}
    <div>
        <p>Quiz complete</p>
        <p>Here is your score: {score}/{shuffledQuestions.length}</p>

        <button on:click={resetQuiz}>Start over?</button>
    </div>
{:else}
    <p>This picture was taken from...</p>
    <div>
        <img src=/images/{shuffledQuestions[activeQuestion].id+1}.jpg alt="" />
    </div>
    <button on:click={() => checkResponse('movie')}>a movie</button>
    <button on:click={() => checkResponse('city')}>the Coronavirus pandemic</button>
{/if}
{#if hasReplied}
    <div>
        {#if isReplyCorrect}
            <p>Good answer, congratulations !</p>
            <p>Do you know from what {shuffledQuestions[activeQuestion].answer} exactly?</p>
            <ul>
            {#each bonusPropositions as proposition, index}
                <li>
                <button on:click={() => checkBonus(proposition.bonus)}>
                    {proposition.bonus}
                </button>
            </li>
            {/each}
            </ul>
        {:else}
            <p>Sorry, incorrect.</p>
            <button on:click={nextQuestion}>Next question</button>
        {/if}
    </div>
{/if}
{#if hasRepliedBonus}
    <div>
        {#if isBonusCorrect}
            <p>Yeah, an extra point for you!</p>
        {:else}
            <p>Nope!</p>
        {/if}

        <button on:click={nextQuestion}>Next question</button>
    </div>
{/if}

<style>
    img {
        width: 400px;
    }
    ul {
        font-size:  1.6rem;
    }
</style>