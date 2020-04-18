<script>
    export let handleClick;
</script>

<div class="quiz-intro">
    <div class="title-emoji"><img src="images/corona.png"> <img src="images/clap.png"></div>
    <h1>COVID-19 or movie ?</h1>
    <p>Can you guess if the following pictures were taken during the 2020 COVID-19 pandemic, or are scenes from a movie ?</p>
    <button on:click={handleClick}>Start the quiz ➔</button>
</div>

<style>
    .quiz-intro {
        margin: 100px auto;
    }

    .title-emoji {
        text-align: center;
    }
    .title-emoji img {
        width: 8rem;
        height: auto;
        vertical-align: middle;
        display: inline-block;
        margin: 0 1rem;
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