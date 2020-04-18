<script>
    export let current;
    export let amount;
</script>
<div>
    Question {current + 1}/{amount}
</div>

<style>
    div {
        position: fixed;
        top: 10px;
        right: 10px;
        background: white;
        color: black;
        padding: 6px;
        font-size: 1.8rem;
        border: 3px solid #000;
    }
    @media (min-width: 750px) {
        div {
            font-size: 2rem;
            padding: 10px;
            border: 4px solid #000;
        }
    }
</style>