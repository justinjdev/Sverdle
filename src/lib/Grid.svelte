<script lang="ts">
	import { pastGuesses, guessOutcomes } from '$lib/stores';
	import Row from '$lib/Row.svelte';
	import { createEventDispatcher } from 'svelte';

	export let answer: string;
	export let rowCount: number;
	export let clickedKey: string;

	let cellCount: number = answer.length;

	let hasWon: boolean = false;
	let hasLost: boolean = false;

	// used for checking guess status
	const answerArr: string[] = answer.split('');

	// tracking the active row
	let activeRow: number = 0;

	// lets the row know which is active for style adjustments
	// could do that here now after refactoring
	let active: boolean[] = [true, ...Array(rowCount - 2).fill(false)];

	// current loc in the answer cell range (0..answer.length-1)
	// reset with each row advancement
	let currIdx = 0;

	// get row# of arrays, filled with cell# empties
	let rowValues: string[][] = Array.from(Array(rowCount), () => Array(cellCount).fill(''));
	let correctValues: boolean[][] = Array.from(Array(rowCount), () => Array(cellCount).fill(false));
	let transposedValues: boolean[][] = Array.from(Array(rowCount), () =>
		Array(cellCount).fill(false)
	);

	const dispatch = createEventDispatcher();

	/**
	 * 0 = correct
	 * 1 = transposed
	 * 2 = wrong
	 */
	function handleGuess(guess: string[]) {
		// make a guess array
		const resArr = [...Array(cellCount).fill(2)];
		for (let i = 0; i < guess.length; i++) {
			if (guess[i] === answerArr[i]) {
				resArr[i] = 0;
			} else if (answerArr.includes(guess[i])) {
				resArr[i] = 1;
			}
			pastGuesses.update((current) => {
				current.add(guess[i]);
				return current;
			});
			guessOutcomes.update((current) => {
				current.set(guess[i], resArr[i]);
				return current;
			});
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

<Row rowNum="0" bind:isActive={active[0]} cells={cellCount} {handleGuess} />
{#each [...Array(rowCount - 1).keys()] as i}
	<Row rowNum={i + 1} bind:isActive={active[i + 1]} cells={cellCount} {handleGuess} />
{/each}
