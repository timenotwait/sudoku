<script>
	import Timer from './Timer.svelte';
	import Actions from './Actions.svelte';
	import TextBox from './TextBox.svelte';
</script>

<div class="action-bar space-x-5">
	<Timer />
	<TextBox />
	<Actions />
</div>

<style>
	.action-bar {
		@apply flex justify-between items-center pb-5;
	}

	@screen xs {
		.action-bar {
			@apply flex-row;
		}
	}
</style>