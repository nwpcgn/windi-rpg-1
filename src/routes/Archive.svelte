<script>
	import PaginationBar from './PaginationBar.svelte'
	import Layer from '../lib/Layer.svelte'
	import { supabase, sleep } from '../lib/data'
	export let name = 'Pagename'
	export let header = 'Header'
	export let body = 'Body'
	let dataDb = []
	let daten = []
	let paginNav = []
	let page_size = 10
	let currentPage = 1
	let numberOfPages = 0

	const paginate = (array, page_size, page_number) =>
		array.slice((page_number - 1) * page_size, page_number * page_size)

	const fetchData = async () => {
		try {
			const { data, error } = await supabase
				.from('bb_clips')
				.select('path,file,size,datum,attr,titel,sammlung,info,daten,id')
			if (error) throw new Error()
			if (data) return data
		} catch (error) {
			alert(error)
		}
	}

	const setPageData = async () => {
		daten = paginate(dataDb, page_size, currentPage)
	}

	const setNav = async () => {
		for (let index = 1; index < numberOfPages + 1; index++) {
			paginNav.push(index)
		}
		console.log('SetNav', paginNav)
		return paginNav
	}

	const initData = async () => {
		dataDb = await fetchData()
		let n = dataDb.length
		numberOfPages = Math.ceil(n / page_size)
		currentPage = 1
		setPageData()
		let arr = await setNav()
		return arr
	}

	const handleNavClick = async (e) => {
		let c = e.currentTarget.dataset.id
		await sleep(200)
		currentPage = c
	}

	let promise = initData()

	$: setPageData(currentPage)
</script>

<Layer glass>
		<header>
			<hgroup>
				<h1>{name}</h1>
				<h3>{header}</h3>
			</hgroup>
		</header>
		<div>
			{#await promise}
				<h1>... loading</h1>
			{:then value}
				<PaginationBar {handleNavClick} bind:currentPage arr={value} />
				<hr />
				<div class="divide-y">
					{#each daten as { path, file, size, datum, attr, titel, sammlung, info, daten, id }, i}
						<div>
							<div>{file}</div>
							<div>{size} byte</div>
						</div>
					{/each}
				</div>
				<hr />
				<PaginationBar {handleNavClick} bind:currentPage arr={value} />
			{/await}
		</div>
</Layer>
