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
        margin-bottom: 5px;
        margin-right: 5px;
    }

    .mapping-key * {
        box-sizing: border-box;
    }

    .plain-key {
        width: 3rem;
        text-align: center;
        font-family: 'Carter One';
        text-transform: capitalize;
        font-size: 1rem;

        color: var(--color-theme-2);

        background-color: var(--color-black);
        outline: none;
        border: none;
    }

    .cipher-key {
        text-align: center;
        padding: 5px;
        width: 3rem;
        font-family: 'Carter One';
        font-size: 1rem;
        
        border: 5px solid var(--color-black);
        outline: none;
    }
</style>