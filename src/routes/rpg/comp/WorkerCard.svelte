<script>
	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()
	export let name = ''
	export let amount = 1
	export let cost = 10
	function onClick() {
		dispatch('click', name)
	}
</script>

<div class="flex items-center gap-2 py-1">
	<button class="w-1/3 btn btn-blue capitalize" on:click={onClick}>Create {name}</button>
	<span>
		<div class="btn">{amount}</div>
	</span>
	<div class="w-1/4 flex flex-col ml-auto align-end capitalize">
		<h6>
			<span>-{cost} Food</span>
		</h6>
		<h6>+1 {name}</h6>
	</div>
</div>