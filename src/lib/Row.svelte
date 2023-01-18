<script>
	import GridCell from './GridCell.svelte';

	export let isActive = false;

	export let cells;
	export let rowNum = '0';

	export let entryValue;

	export let correct;
	export let transposed;
</script>

<div class="row" id="row_{rowNum}" class:active={isActive}>
	{#each [...Array(cells).keys()] as i}
		<GridCell
			id="cell_${i}"
			bind:content={entryValue[i]}
			bind:correct={correct[i]}
			bind:transposed={transposed[i]}
			bind:activeRow={isActive}
		/>
	{/each}
</div>

<style>
	.row {
		display: flex;
		justify-content: center;
	}

	.active {
		scale: 1.02;
	}
</style>
