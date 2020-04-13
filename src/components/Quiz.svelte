<script>
    import movieImages from '../images/movies';
    import lockdownImages from '../images/lockdown';

    let hasReplied = false;
    let imageIndex;
    let isReplyCorrect;

    const buildDataFromImages = (imageFiles, isReal) => (
        Object.entries(imageFiles).map(file => (
            {
                name: file[0],
                source: file[1],
                isReal: isReal
            }
        ))
    );

    const allImages = [
        ...buildDataFromImages(movieImages, false),
        ...buildDataFromImages(lockdownImages, true)
    ];

    const resetQuiz = () => {
        imageIndex = Math.floor(Math.random() * Object.keys(allImages).length);
        hasReplied = false;
        isReplyCorrect = undefined;
    };

    const checkResponse = (isReal) => {
        if (isReal === allImages[imageIndex].isReal) { isReplyCorrect = true }
        else { isReplyCorrect = false };

        hasReplied = true;

        return;
    };

    resetQuiz();
</script>

<p>This picture was taken from...</p>
<div>
    <img src={allImages[imageIndex].source} />
</div>
<button on:click={() => checkResponse(false)}>a movie</button>
<button on:click={() => checkResponse(true)}>the Coronavirus pandemic</button>

{#if hasReplied}
    <div>
        {#if isReplyCorrect}
            <p>Good answer, congratulations !</p>
        {:else}
            <p>Sorry, incorrect.</p>
        {/if}

        <button on:click={resetQuiz}>Try again</button>
    </div>
{/if}

<style>
    img {
        width: 400px;
    }
</style>