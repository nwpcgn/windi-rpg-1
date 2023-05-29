<script>
	import { _game } from '../../../lib/data'
	const chopping_wood_audio = new Audio('/audio/click.mp3')
	const mine_stone_audio = new Audio('/audio/open_001.ogg')
	const mine_iron_audio = new Audio('/audio/click.mp3')
	const gather_food_audio = new Audio('/audio/tick_004.ogg')
	function audioHelper(audioElem) {
		if (audioElem.duration > 0 && !audioElem.paused) {
			//already playing
			audioElem.pause()
			audioElem.currentTime = 0
			audioElem.play()
		} else {
			//not playing
			audioElem.play()
		}
	}
	let audio = {
		wood: chopping_wood_audio,
		stone: mine_stone_audio,
		iron: mine_iron_audio,
		food: gather_food_audio
	}

	$: game = $_game
	$: base_arr = [game.wood, game.stone, game.iron, game.food]
	
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
			console.log(game[slug].amount, game[slug].max)
		}
	}
	function action(slug) {
		game[slug].amount = game[slug].amount + game[slug].clickInc
		check(slug)
		save()
		audioHelper(audio[slug])
	}


</script>

<nav class="space-y-2">
	{#each base_arr as data}
		<div
			class="flex items-center text-3xl gap-2"
			class:opacity-25={data.amount >= data.max}>
			<button
				on:click={() => action(data.name)}
				class="inline-flex items-center gap-2 p-2 border">
				<svg class="icon icon-{data.name}"
					><use xlink:href="#icon-{data.name}" /></svg>
				<span class="text-base capitalize">{data.name}</span>
			</button>

			<span class="ml-auto text-sm">{data.amount}/{data.max} |</span>
			<span class="text-xs">{data.increment}/s</span>
		</div>
	{/each}
</nav>


