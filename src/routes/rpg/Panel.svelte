<script>
	export let open = false
	function toggle() {
		open = !open
	}
</script>

<section class="panel fade center bg-slate-50" class:active={open}>
	<div class="panel__content">
		<slot></slot>
	</div>
</section>


