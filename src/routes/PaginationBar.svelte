<script>
	export let arr = []
	export let currentPage = 1
	export let handleNavClick
</script>

<div class="flex flex-wrap gap-1 py-2">
	{#each arr as item}
		<button
			class="transition-colors duration-200 delay-100 px-2 py-1 rounded shadow"
			class:bg-primary-100={currentPage == item}
			on:click={handleNavClick}
			data-id={item}>{item < 10 ? '0' : ''}{item}</button>
	{/each}
</div>
