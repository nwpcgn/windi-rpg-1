<script>
	import { onMount } from 'svelte'
	import {sleep} from './data'
	export let center = false
	export let glass = false
	export let css = '-translate-x-full'
	export let css_open = 'translate-x-0'
	let open = false
	onMount(async () => {
		await sleep(90)
		open = true
	})
</script>

<section class="layer transform transition-transform duration-200 {open ? css_open : css}" class:center>
	{#if glass}
		<div class="glass"><slot /></div>
	{:else}
		<slot />
	{/if}
</section>
