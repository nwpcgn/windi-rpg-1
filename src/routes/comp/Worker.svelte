<script>
	import WorkerCard from './WorkerCard.svelte'

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

	function createLumberjack() {
		if (worker.amount < worker.max) {
			if (food.amount >= worker.lumberjack.cost) {
				food.amount = food.amount - worker.lumberjack.cost
				worker.amount++
				worker.lumberjack.amount++
				worker.lumberjack.cost++
				wood.increment = worker.lumberjack.increment * worker.lumberjack.amount
				saveStore()
			} else {
				log('Nicht genug Food.', 'info')
			}
		} else {
			log('Nicht genug Unterkünfte', 'error')
		}
	}
	function createMiner() {
		if (worker.amount < worker.max) {
			if (food.amount >= worker.miner.cost) {
				food.amount = food.amount - worker.miner.cost
				worker.amount++
				worker.miner.amount++
				worker.miner.cost++
				stone.increment = worker.miner.increment * worker.miner.amount
				saveStore()
			} else {
				log('Nicht genug Food.', 'info')
			}
		} else {
			log('Nicht genug Unterkünfte', 'error')
		}
	}
	function createScraper() {
		if (worker.amount < worker.max) {
			if (food.amount >= worker.scraper.cost) {
				food.amount = food.amount - worker.scraper.cost
				worker.amount++
				worker.scraper.amount++
				worker.scraper.cost++
				iron.increment = worker.scraper.increment * worker.scraper.amount
				saveStore()
			} else {
				log('Nicht genug Food.', 'info')
			}
		} else {
			log('Nicht genug Unterkünfte', 'error')
		}
	}
	function createHunter() {
		if (worker.amount < worker.max) {
			if (food.amount >= worker.hunter.cost) {
				food.amount = food.amount - worker.hunter.cost
				worker.amount++
				worker.hunter.amount++
				worker.hunter.cost++
				food.increment = worker.hunter.increment * worker.hunter.amount
				saveStore()
			} else {
				log('Nicht genug Food.', 'info')
			}
		} else {
			log('Nicht genug Unterkünfte', 'error')
		}
	}
</script>

<section class="flex flex-col divide-y">
	<WorkerCard {...worker.lumberjack} on:click={createLumberjack} />
	<WorkerCard {...worker.miner} on:click={createMiner} />
	<WorkerCard {...worker.scraper} on:click={createScraper} />
	<WorkerCard {...worker.hunter} on:click={createHunter} />
</section>
