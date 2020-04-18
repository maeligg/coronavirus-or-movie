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
        padding: 10px;
        font-size: 2rem;
        border: 4px solid #000;
    }
</style>