<script>
	import StoreCard from './StoreCard.svelte'

	import StatBar from '../../lib/StatBar.svelte'
	import Layer from '../../lib/Layer.svelte'
	import { addToast } from '../../lib/notes'
	export let wood = {}
	export let stone = {}
	export let iron = {}
	export let food = {}
	export let worker = {}
	export let tent = {}
	export let house = {}
	export let improvedhouse = {}
	export let hostel = {}
	export let saveStore

	const log = (strg, type = 'error') => {
		addToast({ message: strg, type, dismissible: true, timeout: 6000 })
	}

	// Build wood storage buildWoodStorage
	function buildWoodStorage() {
		if (
			wood.amount >= wood.storageCost.wood &&
			stone.amount >= wood.storageCost.stone
		) {
			wood.amount = wood.amount - wood.storageCost.wood
			stone.amount = stone.amount - wood.storageCost.stone
			wood.storage++
			wood.max = wood.max + 100
			saveStore()
		} else {
			log('<p>You need more building materials.</p>')
		}
	}

	// Build stone storage buildStoneStorage
	function buildStoneStorage() {
		if (
			wood.amount >= stone.storageCost.wood &&
			stone.amount >= stone.storageCost.stone
		) {
			wood.amount = wood.amount - stone.storageCost.wood
			stone.amount = stone.amount - stone.storageCost.stone
			stone.storage++
			stone.max = stone.max + 100
			saveStore()
		} else {
			log('<p>You need more building materials.</p>')
		}
	}

	// buildIronStorage

	function buildIronStorage() {
		if (
			wood.amount >= iron.storageCost.wood &&
			stone.amount >= iron.storageCost.stone
		) {
			wood.amount = wood.amount - iron.storageCost.wood
			stone.amount = stone.amount - iron.storageCost.stone
			iron.storage++
			iron.max = stone.max + 100
			saveStore()
		} else {
			log('<p>You need more building materials.</p')
		}
	}

	// Build food storage buildFoodStorage
	function buildFoodStorage() {
		if (
			wood.amount >= food.storageCost.wood &&
			stone.amount >= food.storageCost.stone
		) {
			wood.amount = wood.amount - food.storageCost.wood
			stone.amount = stone.amount - food.storageCost.stone
			food.storage++
			food.max = food.max + 100
			saveStore()
		} else {
			log('<span>You need more building Materials.</span>')
		}
	}
</script>

<section class="flex flex-col divide-y">
	<StoreCard {...wood} on:click={buildWoodStorage} />
	<StoreCard {...stone} on:click={buildStoneStorage} />
	<StoreCard {...iron} on:click={buildIronStorage} />
	<StoreCard {...food} on:click={buildFoodStorage} />
</section>
