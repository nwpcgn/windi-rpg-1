<script>
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
	function buildTent() {
		if (wood.amount >= tent.cost.wood) {
			wood.amount = wood.amount - tent.cost.wood
			tent.amount++
			tent.cost.wood = tent.cost.wood * 1.2
			tent.cost.wood = tent.cost.wood.toFixed(0)
			worker.max = worker.max + tent.residents
			saveStore()
		} else {
			log(`<p>You need more wood.</p>`)
		}
	}
	function buildHouse() {
		if (wood.amount >= house.cost.wood && stone.amount >= house.cost.stone) {
			wood.amount = wood.amount - house.cost.wood
			stone.amount = stone.amount - house.cost.stone
			house.amount++
			house.cost.wood = house.cost.wood * 1.2
			house.cost.stone = house.cost.stone * 1.2
			house.cost.wood = house.cost.wood.toFixed(0)
			house.cost.stone = house.cost.stone.toFixed(0)
			worker.max = worker.max + house.residents
			
			saveStore()
		} else {
			log(`<p>You need more building materials.</p>`)
		}
	}
	function buildImprovedHouse() {
		if (
			wood.amount >= improvedhouse.cost.wood &&
			stone.amount >= improvedhouse.cost.stone &&
			iron.amount >= improvedhouse.cost.iron
		) {
			wood.amount = wood.amount - improvedhouse.cost.wood
			stone.amount = stone.amount - improvedhouse.cost.stone
			iron.amount = iron.amount - improvedhouse.cost.iron
			improvedhouse.amount++
			improvedhouse.cost.wood = improvedhouse.cost.wood * 1.2
			improvedhouse.cost.stone = improvedhouse.cost.stone * 1.2
			improvedhouse.cost.iron = improvedhouse.cost.iron * 1.2
			improvedhouse.cost.wood = improvedhouse.cost.wood.toFixed(0)
			improvedhouse.cost.stone = improvedhouse.cost.stone.toFixed(0)
			improvedhouse.cost.iron = improvedhouse.cost.iron.toFixed(0)
			worker.max = worker.max + improvedhouse.residents
			saveStore()
		} else {
			log(`<p>You need more building materials.</p>`)
		}
	}

	let nIntervId2
	let hostelResearchProg = 100
	let hiddenClass = 'hidden'
	let progressWraphostelClass = hiddenClass

	$: researchHostelClass = op1 ? '' : hiddenClass
	$: buildHostelClass = op1 ? hiddenClass : ''

	function researchHostelProgRun() {
		if (hostelResearchProg <= 100) {
			hostelResearchProg++
		} else {
			progressWraphostelClass = hiddenClass
			hostelResearchProg = 0
			clearInterval(nIntervId2)
		}
	}

	function researchHostelProgStart() {
		hostelResearchProg = 0
		nIntervId2 = setInterval(researchHostelProgRun, 20)
	}
	// Research researchHostel
	function researchHostel() {
		if (wood.amount >= 400 && stone.amount >= 150) {
			wood.amount = wood.amount - 400
			stone.amount = stone.amount - 150
			researchHostelClass = hiddenClass
			progressWraphostelClass = ''
			hostelResearchProg = 0
			researchHostelProgStart()
		} else {
			log('<p>You need more building materials.</p>')
		}
	}
	function researchHostelX() {
		researchHostelClass = hiddenClass
		progressWraphostelClass = ''
		hostelResearchProg = 0
		researchHostelProgStart()
	}
	// Build a hostel buildHostel
	function buildHostel() {
		if (wood.amount >= hostel.cost.wood && stone.amount >= hostel.cost.stone) {
			wood.amount = wood.amount - hostel.cost.wood
			stone.amount = stone.amount - hostel.cost.stone
			hostel.amount++
			hostel.cost.wood = hostel.cost.wood * 1.2
			hostel.cost.stone = hostel.cost.stone * 1.2
			hostel.cost.wood = hostel.cost.wood.toFixed(0)
			hostel.cost.stone = hostel.cost.stone.toFixed(0)
			worker.max = worker.max + hostel.residents
			saveStore()
		} else {
			log('<p>You need more building materials.</p>')
		}
	}
	let op1 = true,
		op2
</script>

<Layer glass>
	<header>
		<StatBar>
			<h2>Buildings</h2>
		</StatBar>
	</header>
	<div class="py-4" />
	<section class="flex flex-col divide-y">
		<!-- Build Tent -->
		<div class="flex items-center gap-2 py-1">
			<button class="btn btn-blue flex-1" on:click={buildTent} id="buildTent"
				>Build Tent</button>
			<span class="flex-1">
				<div class="btn">{tent.amount}</div>
			</span>
			<div class="flex-1 flex flex-col ml-auto items-start">
				<h6>
					<span id="tentCostWood">-{tent.cost.wood} Wood</span>
				</h6>
				<h6>
					<span id="tentResidents">+{tent.residents} Population</span>
				</h6>
			</div>
		</div>
		<!-- Build House -->
		<div class="flex items-center gap-2 py-1">
			<button class="flex-1 btn btn-blue" on:click={buildHouse} id="buildHouse"
				>Build House</button>
			<span class="flex-1">
				<div id="houseAmount" class="btn">{house.amount}</div>
			</span>
			<div class="flex-1 flex flex-col ml-auto items-start">
				<h6 class="flex gap-1">
					<span>-{house.cost.wood} Wood</span>|
					<span>-{house.cost.stone} Stone</span>
				</h6>
				<h6>
					<span>+{house.residents} Population</span>
				</h6>
			</div>
		</div>
		{#if op2}
			<div class="flex items-center gap-2">
				<span>
					<button type="button" id="buildImprovedHouse"
						>Build Improved Housing</button>
				</span>
				<span>
					<button
						type="button"
						id="improvedhouseAmount"
						class="btn btn-blue btn-block"
						disabled>{improvedhouse.amount}</button>
				</span>
				<div class="flex flex-col ml-auto items-start">
					<h6>
						-
						<span id="improvedhouseCostWood">{improvedhouse.cost.wood}</span>
						Wood | -
						<span id="improvedhouseCostStone">0</span>Stone | -
						<span id="improvedhouseCostIron">{improvedhouse.cost.iron}</span
						>Iron
					</h6>
					<h6>
						+
						<span id="improvedhouseResidents">{improvedhouse.residents}</span> Population
					</h6>
				</div>
			</div>
		{/if}
		<!-- Hostel -->
		<div class="flex items-center gap-2 py-1">
			<button
				on:click={researchHostel}
				class="flex-1 btn btn-blue {researchHostelClass}"
				id="researchHostel">Consider Hostels</button>

			<div class="flex-1 {progressWraphostelClass}">
				<input type="range" max={100} min={0} value={hostelResearchProg} />
			</div>

			<button
				on:click={buildHostel}
				id="buildHostel"
				class="flex-1 btn btn-blue {buildHostelClass}">Build Hostel</button>

			<span class="flex-1">
				{#if op1}
					<div id="hostelAmount" class="btn">{hostel.amount}</div>
				{:else}
					<div class="btn opacity-0">{hostel.amount}</div>
				{/if}
			</span>
			<div class="flex-1 flex flex-col ml-auto items-start">
				{#if op1}
					<h6 class="flex gap-1">
						<span id="hostelCostWood">-{hostel.cost.wood} Wood</span>|
						<span id="hostelCostStone">-{hostel.cost.stone} Stone</span>
					</h6>
				{:else}
					<h6 class="flex gap-1">
						<span>-400 Wood</span>|
						<span>-150 Stone</span>
					</h6>
				{/if}
				<h6 class="flex gap-1">
					<span id="hostelResidents">+{hostel.residents} Population</span>
				</h6>
			</div>
		</div>
	</section>
</Layer>
