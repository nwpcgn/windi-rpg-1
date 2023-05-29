<script>
	import { _game } from '../../../lib/data'
	import { onMount, onDestroy } from 'svelte'
	$: game = $_game
	let timer = 10
	let lastSave = 0
	let nIntervId
	let nIntervIdAs

	function save() {
		let update = {
			...$_game,
			...game
		}
		_game.set(update)
	}
	function check(slug) {
		if (game[slug].amount >= game[slug].max) {
			game[slug].amount = game[slug].max
		}
	}

	function tick() {
		action('wood', 'lumberjack')
		action('stone', 'miner')
		action('iron', 'scraper')
		action('food', 'hunter')
	}
	function action(slug, sib) {
		game[slug].increment =
			game.worker[sib].increment * game.worker[sib].amount
		game[slug].amount = game[slug].amount + game[slug].increment

		check(slug)
		save()
	}

	function Timer() {
		if (timer > 0) {
			timer--
		} else {
			lastSave = new Date().toLocaleString()
			timer = 10
			save()
		}
	}
	function beginTick() {
		nIntervId = setInterval(tick, 5000)
	}

	onMount(() => {
		nIntervIdAs = setInterval(Timer, 1000)
		beginTick()
	})
	onDestroy(() => {
		clearInterval(nIntervIdAs)
		clearInterval(nIntervId)
	})


</script>

<div />

<style>
	input[type='text'] {
		@apply w-full py-2 px-2 text-sm text-gray-900 placeholder-gray-400 border border-gray-200 focus:border-primary-500 focus:outline-gray rounded-lg;
	}
	label {
		@apply w-full text-sm font-light;
	}
</style>
