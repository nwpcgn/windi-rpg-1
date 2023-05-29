<script>
	import Layer from '../../lib/Layer.svelte'
	import StatBar from '../../lib/StatBar.svelte'
	import { _game } from '../../lib/data'
	export let wood = {}
	export let stone = {}
	export let food = {}
	export let iron = {}
	export let chopWood, mineStone, mineIron, getFood
	let base_arr = [[wood, chopWood], [stone, mineStone], [iron, mineIron], [food, getFood]]
</script>

<Layer glass>
	<header>
		<StatBar>
			<h2>Generate</h2>
		</StatBar>
	</header>
	<div class="py-4" />
	<div
		class="flex justify-between gap-2 px-2 py-2">
		{#each base_arr as [data, callback]}
			<button class="flex-1 btn btn text-3xl mb-0" on:click={callback} disabled={data.amount >= data.max}>
				<span class="">
					<svg class="icon icon-{data.name}"><use xlink:href="#icon-{data.name}" /></svg>
				</span>
				<span class="capitalize" class:opacity-25={data.amount >= data.max}> {data.name} </span>
			</button>
		{/each}
	</div>
</Layer>


