<script>
	export let content = '';
	export let id = '';
	export let correct = false;
	export let transposed = false;
</script>

<div class="cell" {id} class:transposed class:correct>
	{content}
</div>

<style>
	.cell {
		width: 50px;
		height: 50px;
		border: 1px solid lightcyan;
		margin: 2px;
	}

	.correct {
		border: 1px solid lightgreen;
	}

	.transposed {
		border: 1px solid yellow;
	}
</style>
