<script>
	import Layer from '../lib/Layer.svelte'
	export let name = 'Pagename'
	export let header = 'Header'
	export let body = 'Body'
</script>

<Layer glass>
	<header>
		<hgroup>
			<h1>{name}</h1>
			<h3>{header}</h3>
		</hgroup>

		<p>{@html body}</p>
	</header>
</Layer>
