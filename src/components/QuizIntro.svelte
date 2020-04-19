<script>
    export let handleClick;
</script>

<div class="quiz-intro">
    <div class="title-emoji"><img src="images/corona.png" width="240" height="240" alt="Icon virus"> <img src="images/clap.png" width="240" height="240" alt="Icon movie clapper"></div>
    <h1>COVID-19 or movie?</h1>
    <p>Can you guess if the following pictures were taken during the 2020 COVID-19 pandemic or from movie scenes?</p>
    <button on:click={handleClick}>Start the quiz ➔</button>
</div>

<style>
    .quiz-intro {
        margin: auto;
        text-align: center;
        padding: 50px 0;
    }

    .title-emoji {
        text-align: center;
    }
    .title-emoji img {
        width: 5rem;
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
        line-height: 1.2;
        font-weight: 800;
        text-align: center;
        -webkit-text-stroke: 3px #000;
    }

    p {
        font-size: 2.5rem;
        margin-left: auto;
        margin-right: auto;
        max-width: 600px;
        line-height: 1.15;
    }

    @media (min-width: 750px) {
        h1 {
            font-size: 5rem;
        }
        p {
            font-size: 3rem;
        }
        .title-emoji img {
            width: 8rem;
        }
    }
</style>