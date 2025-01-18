<script>
	import { CANDIDATE_COORDS } from '@sudoku/constants';
	import { UndoRedoManager } from '@sudoku/stores/UndoRedoManager';
	import { stateManager } from '@sudoku/stores/stateManager';
	import { userGrid } from '@sudoku/stores/grid';
	import { SUDOKU_SIZE } from '@sudoku/constants';
	export let candidates = [];
	export let cellX, cellY;


	let currentRemoveCandidate = UndoRedoManager.getRemoveStateCandidate(stateManager.get_index(userGrid.get()));
	if(currentRemoveCandidate) {
		// console.log('currentRemoveCandidate');
		// console.log(currentRemoveCandidate);
		// console.log(cellX, cellY);	// X是列 Y是行
		// console.log(currentRemoveCandidate.get(cellY*SUDOKU_SIZE+cellX));
	}
	
</script>

<div class="candidate-grid">
	{#each CANDIDATE_COORDS as [row, col], index}
		<div class="candidate row-start-{row} col-start-{col} color-visited-{Number(currentRemoveCandidate && currentRemoveCandidate.get(cellY*SUDOKU_SIZE+cellX) && !currentRemoveCandidate.get(cellY*SUDOKU_SIZE+cellX).includes(index + 1))}"
		     class:invisible={!candidates.includes(index + 1)}
		     class:visible={candidates.includes(index + 1)}>
			{index + 1}
		</div>
	{/each}
</div>

<style>
	.candidate-grid {
		@apply grid h-full w-full p-1;
	}

	.candidate {
		@apply h-full w-full row-end-auto col-end-auto leading-full;
	}
	.color-visited-0 {
		background-color: gray;
	}
	.color-visited-1 {

	}


</style>