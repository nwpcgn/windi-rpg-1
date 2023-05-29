<script>
	const topIcon = `<svg viewBox="0 0 90 90" fill="none" role="img" xmlns="http://www.w3.org/2000/svg" class="h-8 w-8"><title>Lucy Stone</title><mask id="mask__ring" maskUnits="userSpaceOnUse" x="0" y="0" width="90" height="90"><rect width="90" height="90" rx="180" fill="#FFFFFF"/></mask><g mask="url(#mask__ring)"><path d="M0 0h90v45H0z" fill="#f5f5f5"/><path d="M0 45h90v45H0z" fill="#e9e9e9"/><path d="M83 45a38 38 0 00-76 0h76z" fill="#e9e9e9"/><path d="M83 45a38 38 0 01-76 0h76z" fill="#0284c7"/><path d="M77 45a32 32 0 10-64 0h64z" fill="#0284c7"/><path d="M77 45a32 32 0 11-64 0h64z" fill="#3b82f6"/><path d="M71 45a26 26 0 00-52 0h52z" fill="#3b82f6"/><path d="M71 45a26 26 0 01-52 0h52z" fill="#f5f5f5"/><circle cx="45" cy="45" r="23" fill="#cccccc"/></g></svg>`
	export let open = false
	export let open2 = false
</script>

<nav class="px-8 py-4 bg-blue-500 sticky top-0 inset-x-0 z-20">
	<div class="flex justify-between items-center">
		<button on:click={() => (open = true)}>
			<svg
				class="h-8 w-8 text-white"
				viewBox="0 0 24 24"
				fill="none"
				stroke="currentColor"
				stroke-width="2"
				stroke-linecap="round"
				stroke-linejoin="round">
				<line x1="3" y1="12" x2="21" y2="12" />
				<line x1="3" y1="6" x2="21" y2="6" />
				<line x1="3" y1="18" x2="21" y2="18" /></svg>
		</button>
		<a class="text-white text-2xl leading-none" href="/">
			{@html topIcon}
		</a>
		<button on:click={() => (open2 = true)}>
			<svg
				class="h-8 w-8 text-white"
				width="24"
				height="24"
				viewBox="0 0 24 24"
				stroke-width="2"
				stroke="currentColor"
				fill="none"
				stroke-linecap="round"
				stroke-linejoin="round">
				<path stroke="none" d="M0 0h24v24H0z" />
				<rect x="4" y="8" width="4" height="4" />
				<line x1="6" y1="4" x2="6" y2="8" />
				<line x1="6" y1="12" x2="6" y2="20" />
				<rect x="10" y="14" width="4" height="4" />
				<line x1="12" y1="4" x2="12" y2="14" />
				<line x1="12" y1="18" x2="12" y2="20" />
				<rect x="16" y="5" width="4" height="4" />
				<line x1="18" y1="4" x2="18" y2="5" />
				<line x1="18" y1="9" x2="18" y2="20" /></svg>
		</button>
	</div>
</nav>

