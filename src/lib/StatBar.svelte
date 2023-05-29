<script>
	import {_game} from './data'
	$: ({
		wood, stone, iron, food, worker
	} = $_game)
</script>

<header class="flex items-center gap-2 py-1">
	<slot><!-- optional fallback --></slot>
	<span class="mr-auto" />
	<span>
		<section>
			<svg class="icon icon-wood"><use xlink:href="#icon-wood" /></svg>
			<span class="sr-only">{wood.name}</span>
			<div>{wood.amount}</div>
		</section>
	</span>
	
	<span>
		<section>
			<svg class="icon icon-stone"><use xlink:href="#icon-stone" /></svg>
			<span class="sr-only">{stone.name}</span>
			<div>{stone.amount}</div>
		</section>
	</span>
	
	<span>
		<section>
			<svg class="icon icon-iron"><use xlink:href="#icon-iron" /></svg>
			<span class="sr-only">{iron.name}</span>

			<div>{iron.amount}</div>
		</section>
	</span>
	
	<span>
		<section class="flex items-center g-1">
			<svg class="icon icon-food"><use xlink:href="#icon-food" /></svg>
			<span class="sr-only">{food.name}</span>

			<div>{food.amount}</div>
		</section>
	</span>

	<span>
		<section>
			<svg class="icon icon-pop"><use xlink:href="#icon-population" /></svg>
			<span class="sr-only">Population</span>
			<div>{worker.amount}</div>
		</section>
	</span>
	
	<span>
		<section>
			<svg class="icon icon-pop-max"><use xlink:href="#icon-maxpop" /></svg>
			<span class="sr-only">Maximale Population</span>
			<div>{worker.max}</div>
		</section>
	</span>
</header>


<style>
	section {
		display: flex;  
		align-items: center;
		gap: 0.45rem;
		font-size: 1.1rem;
	}
	div {
		font-weight: 600;
	}
</style>
