<script>
	export let content = '';
	export let id = '';
	export let correct = false;
	export let transposed = false;
</script>

<div class="cell" {id} class:transposed class:correct>
	{content.toUpperCase()}
</div>

<style>
	.cell {
		width: 50px;
		height: 50px;
		border: 1px solid lightcyan;
		margin: 2px;
		font-family: 'Comic Sans MS';
		display: flex;
		justify-content: center;
		align-items: center;
		color: lightcyan;
		font-size: 2rem;
	}

	.correct {
		border: 1px solid lightgreen;
	}

	.transposed {
		border: 1px solid yellow;
	}
</style>
