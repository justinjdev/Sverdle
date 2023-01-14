<script>
	import Row from '$lib/Row.svelte';

	let rowCount = 5;
</script>

<Row rowNum="0" isActive="true" cells={rowCount} />
{#each [...Array(rowCount - 1).keys()] as i}
	<Row rowNum={i + 1} cells={rowCount} />
{/each}

<style>
</style>
