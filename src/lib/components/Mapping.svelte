<script>
    import { createEventDispatcher } from "svelte";
    import MappingKey from "./MappingKey.svelte";

    const mapping = {};
    const dispatchEvent = createEventDispatcher();

    function handleChange(event) {
        const { cipher, plain } = event.detail;
        mapping[cipher] = plain;

        dispatchEvent('change', {
            mapping: mapping
        });
    }
</script>

<div class="mapping-table">
    {#each Array.from('ABCDEFGHIJKLMNOPQRSTUVWXYZ') as letter}
        <MappingKey cipherKey={letter} on:change={handleChange} />
    {/each}
</div>


<style>
    .mapping-table {
        display: flex;
        flex-direction: column;
        flex-wrap: wrap;
        height: 60vh;
    }
</style>