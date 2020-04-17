<script>
    export let handleClick;
</script>

<div class="quiz-intro">
    <div class="title-emoji">🦠 🎬</div>
    <h1>Coronavirus or movie ?</h1>
    <p>Can you guess if the following pictures were taken during the 2020 Coronavirus pandemic, or are scenes from a movie ?</p>
    <button on:click={handleClick}>Start the quiz ➔</button>
</div>

<style>
    .quiz-intro {
        margin: auto;
    }

    .title-emoji {
        font-size: 8rem;
        text-align: center;
    }

    h1 {
        margin-top: 0;
		text-transform: uppercase;
		color: #fff;
        font-size: 4rem;
        font-weight: 800;
        text-align: center;
        -webkit-text-stroke: 3px #000;
    }

    @media (min-width: 800px) {
        h1 {
            font-size: 5rem;
        }
    }

    p {
        font-size: 2.6rem;
    }

    button {
        float: right;
    }
</style>