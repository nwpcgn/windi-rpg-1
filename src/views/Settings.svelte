<script>
	import { _game } from '../lib/data'
	export let open = false
	export let alphaLayer = 1
	function close() {
		open = false
	}
	function reset() {
		_game.set({
			names: {
				town: 'Gotham City',
				mayor: 'Bruce Wayne'
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
				name: 'Tent',
				slug: 'tent',
				amount: 0,
				residents: 1,
				cost: {
					wood: 30,
					stone: 0,
					iron: 0,
					food: 0
				}
			},
			house: {
				name: 'House',
				slug: 'house',
				amount: 0,
				residents: 4,
				cost: {
					wood: 75,
					stone: 25,
					iron: 0,
					food: 0
				}
			},
			improvedhouse: {
				name: 'Imp. House',
				slug: 'improvedhouse',
				amount: 0,
				residents: 8,
				cost: {
					wood: 200,
					stone: 70,
					iron: 500,
					food: 0
				}
			},
			hostel: {
				name: 'Hostel',
				slug: 'hostel',
				amount: 0,
				residents: 10,
				cost: {
					wood: 200,
					stone: 215,
					iron: 0,
					food: 0
				}
			}
		})
	}
</script>

<section class="panel fade center bg-slate-50" class:active={open}>
	<div class="panel__content">
		<article class="w-full max-w-xs mx-auto px-4 space-y-2">
			<h4>Settings</h4>
			<h5>Alpha Design</h5>
			<div>
				<label>
					<input type="radio" bind:group={alphaLayer} value={0} />
					Layer 1
				</label>
			</div>
			<div>
				<label>
					<input type="radio" bind:group={alphaLayer} value={1} />
					Layer 2
				</label>
			</div>
			<div>
				<label>
					<input type="radio" bind:group={alphaLayer} value={2} />
					Layer 3
				</label>
			</div>
			<button on:click={reset} class="btn btn-blue">Reset Store</button>
			<p>
				<button on:click={close} class="btn btn-blue">Close</button>
			</p>
		</article>
	</div>
</section>
