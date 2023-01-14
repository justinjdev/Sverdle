<script>
	import Row from '$lib/Row.svelte';
	import { createEventDispatcher } from 'svelte';

	export let answer;
	export let rowCount;

	let hasWon = false;
	let hasLost = false;

	const answerArr = answer.split('');
	let activeRow = 0;
	let active = [true, ...Array(rowCount - 2).fill(false)];

	const dispatch = createEventDispatcher();

	/**
	 * @param {string} guess
	 *
	 * 0 = correct
	 * 1 = transposed
	 * 2 = wrong
	 */
	function handleGuess(guess) {
		// make a guess array
		const resArr = [...Array(rowCount).fill(2)];
		for (let i = 0; i < guess.length; i++) {
			if (guess[i] === answerArr[i]) {
				resArr[i] = 0;
			} else if (answerArr.includes(guess[i])) {
				resArr[i] = 1;
			}
		}

		active[activeRow] = false;

		hasWon = resArr.every((elem) => elem == 0);

		if (!hasWon) {
			if (activeRow < rowCount - 1) {
				active[++activeRow] = true;
			} else {
				hasLost = true;
			}
		}

		return resArr;
	}

	$: if (hasWon || hasLost) {
		dispatch('gameOver', { won: hasWon });
	}
</script>

<Row rowNum="0" bind:isActive={active[0]} cells={rowCount} {handleGuess} />
{#each [...Array(rowCount - 1).keys()] as i}
	<Row rowNum={i + 1} bind:isActive={active[i + 1]} cells={rowCount} {handleGuess} />
{/each}

<style>
</style>
