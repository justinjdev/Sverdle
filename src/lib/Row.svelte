<script>
	import GridCell from './GridCell.svelte';

	export let isActive = false;

	export let cells = 6;
	export let rowNum = '0';
	export let entryValue = Array(cells).fill('');

	let correct = Array(cells).fill(false);
	let transposed = Array(cells).fill(false);
</script>

<div class="row" id="row_{rowNum}" class:active={isActive}>
	{#each [...Array(cells).keys()] as i}
		<!-- <div class="cell" id="cell_${i}" content=`${entryValue[i]}`` /> -->
		<GridCell
			id="cell_${i}"
			content={entryValue[i]}
			correct={correct[i]}
			transposed={transposed[i]}
		/>
	{/each}
</div>

<style>
	.row {
		display: flex;
		justify-content: center;
	}
</style>
