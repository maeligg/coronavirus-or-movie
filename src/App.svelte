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
		max-width: 800px;
		margin: 0 auto;
		padding-top: 100px;
	}
</style>
