<script>
	/**
	 * @type {string}
	 */
	export let key;

	function clickToKeypress() {
		document.dispatchEvent(new KeyboardEvent('keydown', { key: key }));
	}
</script>

<button class="key" on:click={clickToKeypress}>
	{key}
</button>

<style>
	.key {
		height: 35px;
		min-width: 40px;
		padding: 0px 2px 0px 2px;
		border: 1px solid lightcyan;
		background-color: #333;
		margin: 1px;
		color: lightcyan;
		display: flex;
		justify-content: center;
		align-items: center;
		cursor: pointer;
		font-family: 'Comis Sans MS';
		font-size: large;
	}
</style>
