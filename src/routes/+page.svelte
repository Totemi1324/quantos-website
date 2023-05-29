<script>
    let title = "Quantos";

    const updateTitle = () => {
        title = "Quantum computing made easy."
    }
</script>

<div class="index">
    <h2>{title}</h2>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Nisi impedit tenetur mollitia commodi ad excepturi similique, cumque consequatur ducimus alias rerum adipisci eaque voluptas magnam iste saepe architecto. Provident odio optio iste! Vitae dolores consectetur ratione, provident, magni similique soluta, at aspernatur rerum a voluptatem! Fugiat minima possimus quae! Doloremque laborum laudantium impedit. Quo voluptatibus rerum deserunt magnam ullam quibusdam!</p>

    <button on:click={updateTitle}>Change title</button>
    <input type="text" bind:value={title}>
</div>

<style>
    .index {
        text-align: center;
        display: block;
        margin: 20px auto;
    }
</style>