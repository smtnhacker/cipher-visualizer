<script>
    import { createEventDispatcher } from "svelte";
    
    export let cipherKey;
    let input = '';
    const dispatchEvent = createEventDispatcher();

    function handleChange(event) {
        dispatchEvent('change', {
            cipher: cipherKey.toLocaleLowerCase(),
            plain: input.toLocaleLowerCase()
        })
    }

</script>

<div class="mapping-key">
    <div class="cipher-key">{cipherKey}</div>
    <input class="plain-key" maxlength="1" type="text" name="plainKey" bind:value={input} on:change={handleChange}>
</div>

<style>
    .mapping-key {
        display: flex;
        margin-bottom: 4px;
    }

    .plain-key {
        width: 50px;
        text-align: center;
    }

    .cipher-key {
        text-align: center;
        padding: 5px;
        width: 20px;
    }
</style>