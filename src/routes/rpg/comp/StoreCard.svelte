<script>
	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()
	export let name = ''
	// export let increment = 1
	// export let amount = 0
	// export let max = 100
	export let storage = 0
	export let storageCost = {
		wood: 50,
		stone: 50
	}
	function onClick() {
		dispatch('click', name)
	}
</script>

<div class="flex items-center gap-2 py-1">
		<button on:click={onClick} class="w-1/3 btn btn-blue capitalize">Build {name} Storage</button>
		<span>
			<div
				id="{name}Amount"
				class="btn" disabled>{storage}</div>
		</span>
		<div class="w-1/4 flex flex-col ml-auto capitalize">
			<h6 class="flex gap-1">
				<span>-{storageCost.wood} Wood</span>
				|
				<span>-{storageCost.stone} Stone</span>
			</h6>
			<h6>+100 {name} Storage</h6>
		</div>
	</div>

