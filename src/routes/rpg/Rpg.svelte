<script>
	import Engine from './comp/Engine.svelte'
	import AlphaGrid from './comp/AlphaGrid.svelte'
	import StatBar from './comp/StatBar.svelte'
	import Panel from './Panel.svelte'
	import Generate from './comp/Generate.svelte'
	import Worker from './comp/Worker.svelte'
	import Build from './comp/Build.svelte'
	import Store from './comp/Store.svelte'
	import Window from './Window.svelte'
	import { addToast } from '../../lib/notes'
	import { Route, router } from 'tinro'
	import { _game } from '../../lib/data'
	
	$: game = {
		names: {
			town: '',
			mayor: ''
		},
		wood: {
			name: 'wood',
			slug: 'wood',
			clickInc: 1,
			amount: 0,
			increment: 0,
			max: 100,
			storage: 0,
			storageCost: {
				wood: 50,
				stone: 50
			}
		},
		stone: {
			name: 'stone',
			slug: 'stone',
			clickInc: 1,
			amount: 0,
			increment: 0,
			max: 100,
			storage: 0,
			storageCost: {
				wood: 50,
				stone: 50
			}
		},
		iron: {
			name: 'iron',
			slug: 'iron',
			clickInc: 1,
			amount: 0,
			increment: 0,
			max: 100,
			storage: 0,
			storageCost: {
				wood: 100,
				stone: 100
			}
		},
		food: {
			name: 'food',
			slug: 'food',
			clickInc: 1,
			amount: 0,
			increment: 0,
			max: 100,
			storage: 0,
			storageCost: {
				wood: 50,
				stone: 50
			}
		},
		worker: {
			name: 'worker',
			amount: 0,
			max: 0,
			lumberjack: {
				name: 'Lumberjack',
				increment: 1,
				amount: 0,
				cost: 10
			},
			miner: {
				name: 'Miner',
				increment: 1,
				amount: 0,
				cost: 10
			},
			scraper: {
				name: 'Scraper',
				increment: 1,
				amount: 0,
				cost: 10
			},
			hunter: {
				name: 'Hunter',
				increment: 1,
				amount: 0,
				cost: 10
			}
		},
		tent: {
			amount: 0,
			residents: 1,
			cost: {
				wood: 30
			}
		},
		house: {
			amount: 0,
			residents: 4,
			cost: {
				wood: 75,
				stone: 25
			}
		},
		improvedhouse: {
			amount: 0,
			residents: 8,
			cost: {
				wood: 200,
				stone: 70,
				iron: 500
			}
		},
		hostel: {
			amount: 0,
			residents: 10,
			cost: {
				wood: 200,
				stone: 215
			}
		}
	}

	function saveStore() {
		let update = {
			...$_game,
			...game
		}
		_game.set(update)
	}
	const log = (message, type = 'info', dismissible = true, timeout = 5000) => {
		// let types = ['success', 'error', 'info']
		addToast({ message, type, dismissible, timeout })
	}

	$: base_arr = [$_game.wood, $_game.stone, $_game.iron, $_game.food]
	export let open = false
	export let alphaLayer = 1
	function toggle() {
		open = !open
	}
	let nav = [
		{ titel: 'Generate', icon: 'generate', path: '/rpg/generate', cn: 's1' },
		{ titel: 'Build', icon: 'build', path: '/rpg/build', cn: 's2' },
		{ titel: 'Store', icon: 'store', path: '/rpg/store', cn: 's3' },
		{ titel: 'Worker', icon: 'worker', path: '/rpg/worker', cn: 's4' }
	]
	const closeWindow = () => {
		router.goto('/rpg')
	}
</script>

<Panel bind:open>
	<article class="w-full max-w-lg mx-auto p-4">
		<div class="glass">
			<h4>Settings</h4>
			<nav class="p-2 bg-white rounded">
				<h5>Rpg Game</h5>
				<hr />
				<label>Town</label>
				<input
					type="text"
					value={game.names.town}
					on:blur={(e) => {
						game.names.town = e.currentTarget.value
					}} />
				<label>Major</label>
				<input
					type="text"
					value={game.names.mayor}
					on:blur={(e) => {
						game.names.mayor = e.currentTarget.value
					}} />
				<div class="py-1" />
				<button
					on:click={() => {
						saveStore()
						log('Game saved!', 'success')
					}}
					class="btn btn-blue">Save</button>
			</nav>
			<div class="py-4" />
			<div class="space-y-2 p-2 bg-white rounded">
				<h5>Rohstoffe</h5>
				<hr />
				{#each base_arr as { name, amount, increment, max, storage }}
					<div class="flex items-center text-2xl gap-2">
						<svg class="icon icon-{name}"
							><use xlink:href="#icon-{name}" /></svg>
						<span class="text-base capitalize">{name}</span>
						<span class="ml-auto text-sm">{amount}/{max} |</span>
						<span class="text-xs">{increment}/s</span>
					</div>
				{/each}
			</div>
			<p>
				<button on:click={toggle} class="btn btn-blue">Close</button>
			</p>
		</div>
	</article>
</Panel>
<Engine />
<main class="main">
	<AlphaGrid bind:layer={alphaLayer} bind:nav />
	<header class="absolute z-10 top-0 left-0">
		<div>
			<button class="btn btn-blue" on:click={toggle}>Toggle</button>
		</div>
	</header>
	<Route path="/generate">
		<Window on:click={closeWindow}>
			<Generate />
		</Window>
	</Route>
	<Route path="/build">
		<Window on:click={closeWindow}>
			<svelte:component this={Build} {...game} {saveStore} />
		</Window>
	</Route>
	<Route path="/store">
		<Window on:click={closeWindow}>
			<svelte:component this={Store} {...game} {saveStore} />
		</Window>
	</Route>
	<Route path="/worker">
		<Window on:click={closeWindow}>
			<svelte:component this={Worker} {...game} {saveStore} />
		</Window>
	</Route>
	<div class="absolute z-10 inset-x-0 bottom-0">
		<StatBar />
	</div>

	<!-- <aside class="min-w-72 lg:min-w-80">
	<section class="layer">
		<div class="glass">
			<nav class="p-2 bg-white rounded">
				<h5>Rpg Game</h5>
				<hr />
				<label>Town</label>
				<input
					type="text"
					value={game.names.town}
					on:blur={(e) => {
						game.names.town = e.currentTarget.value
					}} />
				<label>Major</label>
				<input
					type="text"
					value={game.names.mayor}
					on:blur={(e) => {
						game.names.mayor = e.currentTarget.value
					}} />
				<div class="py-1" />
				<button
					on:click={() => {
						saveStore()
						log('Game saved!', 'success')
					}}
					class="btn btn-blue">Save</button>
			</nav>
			<div class="py-4" />
			<div class="space-y-2 p-2 bg-white rounded">
				<h5>Rohstoffe</h5>
				<hr />
				{#each base_arr as { name, amount, increment, max, storage }}
					<div class="flex items-center text-2xl gap-2">
						<svg class="icon icon-{name}"
							><use xlink:href="#icon-{name}" /></svg>
						<span class="text-base capitalize">{name}</span>
						<span class="ml-auto text-sm">{amount}/{max} |</span>
						<span class="text-xs">{increment}/s</span>
					</div>
				{/each}
			</div>
		</div>
	</section>
</aside> -->
</main>

<style>
	input[type='text'] {
		@apply w-full py-2 px-2 text-sm text-gray-900 placeholder-gray-400 border border-gray-200 focus:border-primary-500 focus:outline-gray rounded-lg;
	}
	label {
		@apply w-full text-sm font-light;
	}
</style>
