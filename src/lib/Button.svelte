<script>
	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()
	function onClick(e) {
		dispatch('click', {
			el: e.currentTarget
		})
	}
	export let color = 'blue'
	export let href = false
	export let full = false
	export let disabled = false
</script>

{#if href}
	<a
		{href}
		on:click={onClick}
		class="button {color}"
		class:btn-full={full}
		class:disabled
		{...$$restProps}><slot /></a>
{:else}
	<button
		on:click={onClick}
		class="button {color}"
		class:btn-full={full}
		class:disabled
		type="button"
		{disabled}
		{...$$restProps}><slot /></button>
{/if}

<style>
	.button {
		@apply px-5 py-3 text-sm font-semibold rounded transition duration-200;
	}
	.button-full {
		@apply block w-full text-center;
	}
	.button.blue {
		@apply border bg-blue-500 hover:bg-blue-600 text-white border-blue-500 hover:border-blue-600;
	}
	.button.light {
		@apply border text-blue-500 hover:text-white hover:bg-blue-500 border-blue-500 hover:border-blue-600;
	}
	.button[disabled],
	.button.disabled {
		@apply opacity-25 cursor-default;
	}
</style>
