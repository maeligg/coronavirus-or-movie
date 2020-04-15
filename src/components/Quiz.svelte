<script>
    import questions from '../data/questions';

    let hasReplied = false;
    let activeQuestion = 0;
    let isReplyCorrect;
    let score = 0;

    const checkResponse = (from) => {
        if (from === questions[activeQuestion].answer) {
            isReplyCorrect = true;
            score++;
        }

        hasReplied = true;
        return;
    };

    const nextQuestion = () => {
        hasReplied = false;
        activeQuestion++;
    };

    const resetQuiz = () => {
        questions.sort(() => Math.random() - 0.5);
        activeQuestion = 0;
    };
    resetQuiz();
</script>

{#if activeQuestion === questions.length}
    <div>
        <p>Quiz complete</p>
        <p>Here is your score: {score}/{questions.length}</p>

        <button on:click={resetQuiz}>Start over?</button>
    </div>
{:else}
    <h2>This picture was taken from...</h2>
    <div>
        <img src=/images/{questions[activeQuestion].id+1}.jpg />
    </div>
    <div class="buttons-wrapper">
        <button on:click={() => checkResponse('movie')}>🎬 a movie</button>
        <button on:click={() => checkResponse('city')}>🦠 the Coronavirus pandemic</button>
    </div>
{/if}
{#if hasReplied}
    <div>
        {#if isReplyCorrect}
            <p>Good answer, congratulations !</p>
            <p>Do you know from what {questions[activeQuestion].answer} exactly?</p>
            <ul>
            {#each questions[activeQuestion].bonus as answer}
                <li>{answer}</li>
            {/each}
            </ul>
        {:else}
            <p>Sorry, incorrect.</p>
        {/if}

        <button on:click={nextQuestion}>Next question</button>
    </div>
{/if}

<style>
    h2 {
		color: #fff;
        font-size: 4rem;
        font-weight: 800;
        text-align: center;
        -webkit-text-stroke: 2px #000;
    }
    
    img {
        width: 100%;
    }

    .buttons-wrapper {
        margin-top: 10px;
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
    }

    ul {
        font-size:  1.6rem;
    }
</style>