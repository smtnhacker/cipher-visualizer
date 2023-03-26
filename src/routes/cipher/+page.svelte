<script>
	import Mapping from '$lib/components/Mapping/Mapping.svelte';

	let input = '';
	let mapping = {};

	$: cipher = input.toLocaleLowerCase();
	$: {
		const freq = {}
		Array.from(cipher).forEach(e => {
			if (freq[e] === undefined) {
				freq[e] = 1;
			} else {
				freq[e] += 1;
			}
		})
		const percentage = Object.keys(freq).map(l => {
			if (l === ' ' || l === '\n' || l === '\'' || l === ',' || l === '?' || l === '-') {
				return [0, l];
			} else {
				return [freq[l], l];
			}
		}).sort((a, b) => a[0] - b[0]);
		console.log(percentage)
	}

	function handleChange(event) {
		mapping = { ...event.detail.mapping };
		console.log(mapping);
	}
</script>

<svelte:head>
	<title>Cipher Visualizer</title>
	<meta name="description" content="To help you solve some ciphers!" />
</svelte:head>

<section>
	<div class="container">
		<div class="left">
			<textarea 
				class="input" 
				spellcheck={false} 
				bind:value={input} 
				name="cipher" 
				rows="10"
				placeholder="Enter the cipher text"></textarea>
			<div class="decoded">
				{#each Array.from(cipher) as letter}
					{#if letter === '\n'}
						<br />
					{:else if mapping[letter] === undefined || mapping[letter] === ''}
						<span>{letter}</span>
					{:else}
						<span style="color: var(--color-theme-1)">{mapping[letter]}</span>
					{/if}
				{/each}
			</div>
		</div>
        <div>
            <div class="sticky">
                <Mapping on:change={handleChange} />
            </div>
        </div>
	</div>
</section>

<style>
    textarea {
        padding: 10px;
    }
	.container {
		display: flex;
        justify-content: center;
		max-width: 70%;
		margin-left: auto;
		margin-right: auto;
		padding: 3rem;
	}
	.container * {
		box-sizing: border-box;
	}
	.left {
		min-width: 80%;
	}
	.input {
		font-family: 'Carter One';
		font-weight: 400;
		text-decoration: none;
		color: white;
		background-color: #565559;
		border-radius: 20px;
		outline: none;
		padding: 2rem;
		width: 80%;
	}
    .decoded {
        margin-top: 12px;
        padding: 12px;

		font-family: 'Carter One';
		font-weight: 400;
        font-size: 1.2em;

		background-color: #F5F5F5;
		border-radius: 32px;
		width: 80%;
		padding: 2rem;
    }
    .sticky {
        position: sticky;
        top: 2rem;
		min-width: 20%;
    }
    
</style>
