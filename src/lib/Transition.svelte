<script>
	import { router } from 'tinro'
	import { fade } from 'svelte/transition'
</script>

{#key $router.path}
	<article out:fade={{ duration: 300 }}>
		<slot />
	</article>
{/key}
