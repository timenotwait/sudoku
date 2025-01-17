<script>
	import { onMount } from 'svelte';
	import { BASE_URL } from '@sudoku/constants';
	import { modal } from '@sudoku/stores/modal';
	import { userGrid, grid, strategySolution } from '@sudoku/stores/grid';
	import Clipboard from '../../Utils/Clipboard.svelte';

	export let data = {};
	export let hideModal;

	const sencode = grid.getSencode($userGrid, $strategySolution);
	const origin_sencode = grid.getOriginSencode($grid);

	const link = sencode;
	const encodedLink = encodeURIComponent(link);
	const facebookLink = 'https://www.facebook.com/sharer/sharer.php?u=' + encodedLink;
	const twitterLink = 'https://twitter.com/intent/tweet?text=Check%20out%20this%20Sudoku%20puzzle!&url=' + encodedLink;
	const mailToLink = 'mailto:?subject=A%20Sudoku%20puzzle%20for%20you&body=Here%27s%20a%20link%20to%20a%20Sudoku%20puzzle%20on%20sudoku.jonasgeiler.com%3A%0A%0A' + encodedLink;

	let copyText;

	function select(element) {
		element.select();
		element.setSelectionRange(0, element.value.length);
	}

	onMount(() => {
		let canShare = false;
		const shareData = {
			url: link,
			title: 'Sudoku',
			text: 'Create & play Sudoku puzzles on sudoku game!'
		};

		if ('share' in navigator) {
			canShare = true;
		}

		if ('canShare' in navigator) {
			canShare = navigator.canShare(shareData);
		}

		if (canShare) {
			navigator.share(shareData);
		}
	});
</script>

<div class="flex justify-between items-center mb-6">
	<h1 class="text-3xl font-semibold leading-none">Share Sudoku</h1>

	<div class="cursor-pointer" on:click={hideModal}>
		<svg class="icon-outline" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
			<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
		</svg>
	</div>
</div>

<div class="code-container">
	<input class="input code-field" type="text" readonly value={sencode} on:click={e => select(e.target)}>

	<button class="btn btn-copy" on:click={copyText(sencode)}>
		<svg class="icon-outline" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
			<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 5H6a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2v-1M8 5a2 2 0 002 2h2a2 2 0 002-2M8 5a2 2 0 012-2h2a2 2 0 012 2m0 0h2a2 2 0 012 2v3m2 4H10m0 0l3-3m-3 3l3 3" />
		</svg>
	</button>
</div>

<div class="code-container">
	<input class="input code-field" type="text" readonly value={origin_sencode} on:click={e => select(e.target)}>

	<button class="btn btn-copy" on:click={copyText(origin_sencode)}>
		<svg class="icon-outline" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
			<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 5H6a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2v-1M8 5a2 2 0 002 2h2a2 2 0 002-2M8 5a2 2 0 012-2h2a2 2 0 012 2m0 0h2a2 2 0 012 2v3m2 4H10m0 0l3-3m-3 3l3 3" />
		</svg>
	</button>
</div>


<hr class="my-8" />

<div class="flex flex-col space-y-2">

	<a href={link} class="btn btn-small" on:click|preventDefault={copyText(link)}>
		<svg class="icon-outline mr-2" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
			<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.101m-.758-4.899a4 4 0 005.656 0l4-4a4 4 0 00-5.656-5.656l-1.1 1.1" />
		</svg>

		<span>Copy Link</span>
	</a>
</div>

<Clipboard bind:copyText />

<style>
	.code-container {
		@apply flex flex-col;
	}

	.code-field {
		@apply rounded-b-none font-mono text-center;
	}

	.btn-copy {
		@apply p-3 rounded-t-none;
	}

	@screen sm {
		.code-container {
			@apply flex-row;
		}

		.code-field {
			@apply flex-grow rounded-bl-xl rounded-r-none;
		}

		.btn-copy {
			@apply rounded-tr-xl rounded-l-none;
		}
	}


	.btn-share {
		@apply text-white border-none;
	}

	.btn-share-twitter {
		background-color: #1da1f2;
	}

	.btn-share-twitter:hover {
		background-color: #1a91da;
	}

	.btn-share-twitter:active {
		background-color: #1781c2;
	}

	.btn-share-facebook {
		background-color: #1877f2;
	}

	.btn-share-facebook:hover {
		background-color: #166bda;
	}

	.btn-share-facebook:active {
		background-color: #135fc2;
	}
</style>