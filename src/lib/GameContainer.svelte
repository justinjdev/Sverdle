<script>
	import Grid from './Grid.svelte';
	import Keyboard from './keyboard/Keyboard.svelte';

	let isOver = false;
	let didWin = false;
	let answer = 'crate';

	function handleGameOver(e) {
		isOver = true;
		didWin = e.detail.won;
	}
</script>

<Grid on:gameOver={handleGameOver} {answer} rowCount={answer.length} />

<div class:hidden={!isOver} class="msg-wrapper" class:won={didWin}>
	{didWin ? 'Congratulations!' : 'Maybe next time :('}
</div>

<div class="kbContainer">
	<Keyboard on:keydown={() => console.log('something')} />
</div>

<style>
	.kbContainer {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 200px;
	}

	.hidden {
		opacity: 0%;
	}

	.msg-wrapper {
		font-family: 'Comic Sans MS';
		text-align: center;
		color: palevioletred;
	}

	.won {
		color: greenyellow;
	}
</style>
