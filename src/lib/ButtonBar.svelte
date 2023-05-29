<script>
    import {slide} from 'svelte/transition'
    const slideOp = {duration: 400}
</script>

<nav in:slide={slideOp} class="inline-flex items-center gap-1 flex-wrap">
	<slot />
</nav>
