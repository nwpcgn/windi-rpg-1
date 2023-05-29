<script>
	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()
	function onClick(e) {
		dispatch('click', {
			el: e.currentTarget
		})
	}
	export let label = 'Rpg-Game'
</script>

<div class="absolute z-20 inset-x-0 top-0 p-4">
	<nav class="bg-white rounded-md border-2 border-slate-400">
		<h5 class="flex items-center justify-between py-2 px-4">
			<span>{label}</span>
			<button on:click={onClick}>
				<svg class="icon icon-close"><use xlink:href="#icon-close" /></svg>
			</button>
		</h5>
		<hr />
		<div class="py-2 px-4">
			<slot />
		</div>
	</nav>
</div>
