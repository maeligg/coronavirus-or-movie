<script>
    export let handleClick;
</script>

<div>
    <h1>🦠 <span class="title-inner">Coronavirus or movie ?</span> 🎬</h1>
    <p>Can you guess if the following pictures were taken during the 2020 Coronavirus pandemic, or are scenes from a movie ?</p>
    <button on:click={handleClick}>Start the quiz ➔</button>
</div>

<style>
    h1 {
		text-transform: uppercase;
		color: #fff;
        font-size: 4rem;
        font-weight: 800;
        text-align: center;
    }

    @media (min-width: 800px) {
        h1 {
            font-size: 5rem;
        }
    }
    
    .title-inner {
        -webkit-text-stroke: 3px #000;
    }

    p {
        font-size: 2.6rem;
    }

    button {
        float: right;
    }
</style>