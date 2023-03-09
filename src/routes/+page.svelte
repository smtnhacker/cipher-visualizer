<script>
	import Mapping from '$lib/components/Mapping.svelte';

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
	<h1>Cipher Visualizer</h1>
	<div class="container">
		<div class="left">
			<textarea bind:value={input} name="cipher" cols="30" rows="10"></textarea>
			<div>
				{#each Array.from(cipher) as letter}
					{#if letter === '\n'}
						<br />
					{:else if mapping[letter] === undefined || mapping[letter] === ''}
						<span>{letter}</span>
					{:else}
						<span style="color: red">{mapping[letter]}</span>
					{/if}
				{/each}
			</div>
		</div>
		<Mapping on:change={handleChange} />
	</div>
</section>

<style>
	.container {
		display: flex;
	}
</style>


