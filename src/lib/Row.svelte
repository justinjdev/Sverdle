<script>
	import { createEventDispatcher } from 'svelte';
	import GridCell from './GridCell.svelte';

	export let isActive = false;

	export let cells = 6;
	export let rowNum = '0';
	export let handleGuess;

	let entryValue = Array(cells).fill('');
	let currIdx = 0;

	let correct = Array(cells).fill(false);
	let transposed = Array(cells).fill(false);

	function dealWithGuessFallout() {
		const resArr = handleGuess(entryValue);
		resArr.forEach((element, idx) => {
			if (element == 0) {
				correct[idx] = true;
			} else if (element == 1) {
				transposed[idx] = true;
			}
		});
	}

	function keydown(e) {
		if (!isActive) {
			return;
		}

		if (e.key === 'Enter') {
			if (currIdx != cells) {
				// don't let enter if we're not full
				return;
			}
			dealWithGuessFallout();
			return;
		}

		if (e.key === 'Backspace' && currIdx > 0) {
			currIdx -= 1;
			entryValue[currIdx] = '';
			return;
		}

		if (currIdx == cells) {
			return;
		}

		if ((e.keyCode >= 65 && e.keyCode <= 90) || (e.keyCode >= 97 && e.keyCode <= 122)) {
			entryValue[currIdx] = e.key;
			currIdx += 1;
			return;
		}
	}
</script>

<svelte:window on:keydown={keydown} />
<div class="row" id="row_{rowNum}" class:active={isActive}>
	{#each [...Array(cells).keys()] as i}
		<GridCell
			id="cell_${i}"
			content={entryValue[i]}
			correct={correct[i]}
			transposed={transposed[i]}
			activeRow={isActive}
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
