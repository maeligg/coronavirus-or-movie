<script>
    export let handleClick;
</script>

<div>
    <h1>Coronavirus or movie ?</h1>
    <p>Can you guess if the following pictures were taken during the 2020 Coronavirus pandemic, or are scenes from a movie ?</p>
    <button on:click={handleClick}>Start the quiz</button>
</div>

<style>
    h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4rem;
		font-weight: 100;
	}
</style>