<script lang="ts">
	import Child from './Child.svelte';
	let name = 'Svelte';
	let inputs = creatObj(8);
	let _refs = [];
	let value = 0;
	$: filterList = inputs.filter(m => m.selected);
	$: if ( filterList.length >= 0) {
		value = reduceFunction();
	}
	function creatObj(count) {
		const p = [];
		for(let i = 0; i < count; i++) {
			p.push(
				{
					item: i,
					key: i,
					value: 0,
					selected: false
				}
			);
		}
		return p;
	}
	const reduceFunction = () => {
		if (filterList.length) {
			return filterList.map(m => m.value).reduce((previousValue, currentValue) => previousValue + currentValue);
		} 
		return 0;
	}
	const resetList = () => {
		for(let item of inputs) {
			item.selected = false;
		}
	}
</script>

<main>
	<h2>Hello {name}!</h2>
	<div style="display: flex; width: 100%">
		{#each inputs as input, i}
			<Child reset={resetList} bind:this={_refs[i]} bind:value={input.value} bind:selected={input.selected}/>
		{/each}

	</div>
	<h1>
		{value}
	</h1>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>