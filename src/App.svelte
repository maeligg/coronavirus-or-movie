<script>
	import QuizIntro from './components/QuizIntro.svelte';
	import Quiz from './components/Quiz.svelte';

	let quizStarted = false;
	const startQuiz = () => quizStarted = true;
</script>

<main>
	{#if !quizStarted}
		<QuizIntro handleClick={startQuiz} />
	{:else}
		<Quiz />
	{/if}
</main>

<style>
	main {
		display: flex;
		flex-direction: column;
		min-height: 100%;
		max-width: 880px;
		margin: 0 auto;
		padding: 0 20px;
	}
</style>
