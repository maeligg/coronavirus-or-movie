<script>
    export let totalQuestions, score, scoreBonus, resetQuiz;
</script>

<div class="quiz-results">
    <h3>Quiz complete</h3>
    <p>Your final score: {score} / {totalQuestions}</p>
    <p>Bonus points: {scoreBonus} / {totalQuestions}</p>

    <div class="buttons-wrapper">
        <button on:click={resetQuiz} class="reset-quiz">Start over?</button>
        <a href="https://twitter.com/intent/tweet?text=I+played+'COVID-19+or+Movie'+on+https://covid19-or-movie.pizza/+I+got+{score}+points+and+{scoreBonus}+bonus+points+!" target="_blank" rel="noopener" class="button twitter-share-button">
            <img src="./images/twitter.svg" alt="twitter" class="twitter-icon" />
            Share on Twitter
        </a>    </div>
</div>

<style>
    .quiz-results {
        margin: auto;
        padding: 20px;
        background: #fff;
        border: 3px solid #000;
    }

    h3 {
        margin-top: 0;
        color: #000;
        font-size: 3rem;
    }

    .buttons-wrapper {
        display: flex;
    }

    .twitter-share-button {
        display: flex;
        align-items: center;
    }

    .reset-quiz {
        margin-right: 10px;
    }

    .twitter-icon {
        height: 20px;
        margin-right: 6px;
    }
    @media (min-width: 750px) {
        .quiz-results {
            border: 4px solid #000;
        }
    }
</style>

