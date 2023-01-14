<script>
	import Grid from './Grid.svelte';
	import Keyboard from './keyboard/Keyboard.svelte';
</script>

<Grid />

<div class="kbContainer">
	<Keyboard />
</div>

<style>
	.kbContainer {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 200px;
	}
</style>
