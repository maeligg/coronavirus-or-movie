<script>
	import QuizIntro from './components/QuizIntro.svelte';
	import Quiz from './components/Quiz.svelte';
    import questions from './data/questions';

	let quizStarted = false;
	const startQuiz = () => quizStarted = true;

    const preloadImg = (url) => {
        const img = new Image();
        img.src = url;
    }

    questions.forEach(q => preloadImg(`/images/${q.id + 1}.jpg`));
</script>
<main>
	{#if !quizStarted}
		<QuizIntro handleClick={startQuiz} />
	{:else}
		<Quiz />
	{/if}
	<a href="https://github.com/maeligg/coronavirus-or-movie/blob/master/README.md" target="_blank" rel="noopener">About</a>
</main>

<style>
	main {
		display: flex;
		flex-direction: column;
		min-height: 100%;
		max-width: 880px;
		margin: 0 auto;
		padding: 0 20px;
		position: relative;
		z-index: 1;
	}

	a {
        margin-bottom: 10px;
        text-align: center;
        font-size: 1.6rem;
    }
</style>
