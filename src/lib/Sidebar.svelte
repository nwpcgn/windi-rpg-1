<script>
	import { clickOutside } from '../lib/data'
	const sbIcon = `<svg class="w-8 h-8" viewBox="0 0 80 80" fill="none" role="img" xmlns="http://www.w3.org/2000/svg"><title>Carrie Chapman</title><mask id="mask__bauhaus" maskUnits="userSpaceOnUse" x="0" y="0" width="80" height="80"><rect width="80" height="80" rx="160" fill="#FFFFFF"/></mask><g mask="url(#mask__bauhaus)"><rect width="80" height="80" fill="#3b82f6"/><rect x="10" y="30" width="80" height="10" fill="#cccccc" transform="translate(16 -16) rotate(336 40 40)"/><circle cx="40" cy="40" fill="#f5f5f5" r="16" transform="translate(-18 18)"/><line x1="0" y1="40" x2="80" y2="40" stroke-width="2" stroke="#e9e9e9" transform="translate(12 12) rotate(312 40 40)"/></g></svg>`
	const closeBtn = `<svg class="h-6 w-6 cursor-pointer hover:text-blue-500" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>`
	export let open = false
	function close() {
		open = false
	}
</script>

<div
	class="navbar-backdrop fixed inset-0 bg-black text-gray-800 opacity-25"
	class:hidden={!open} />
<aside
	use:clickOutside
	on:click_outside={close}
	class="navbar-menu fixed top-0 left-0 bottom-0 w-5/6 max-w-sm z-40 transform duration-300 transition-transform ease-in-out {open
		? 'translate-x-0'
		: '-translate-x-full'}">
	<nav
		class="relative flex flex-col py-6 px-6 w-full h-full bg-white border-r overflow-y-auto">
		<div class="flex items-center mb-12">
			<a class="mr-auto text-2xl font-semibold leading-none" href="/">
				{@html sbIcon}
			</a>
			<button class="navbar-close" on:click={close}>
				{@html closeBtn}
			</button>
		</div>
		<div>
			<ul>
				<li class="mb-1">
					<a
						class="block p-4 text-sm font-semibold hover:bg-blue-50 hover:text-blue-500 rounded"
						href="/">Start</a>
				</li>
				<li class="mb-1">
					<a
						class="block p-4 text-sm font-semibold hover:bg-blue-50 hover:text-blue-500 rounded"
						href="/bj">Blackjack</a>
				</li>
				<li class="mb-1">
					<a
						class="block p-4 text-sm font-semibold hover:bg-blue-50 hover:text-blue-500 rounded"
						href="/info">Services</a>
				</li>
				<li class="mb-1">
					<a
						class="block p-4 text-sm font-semibold hover:bg-blue-50 hover:text-blue-500 rounded"
						href="/rpg">Rpg</a>
				</li>
			</ul>
		</div>
		<div class="mt-auto">
			<div class="pt-6">
				<button
					class="block w-full px-5 py-3 mb-3 text-sm text-center bg-blue-500 hover:bg-blue-600 text-white font-semibold border border-blue-500 hover:border-blue-600 rounded transition duration-200"
					>Sign in</button
				><button
					class="block w-full px-5 py-3 text-sm text-center font-semibold text-blue-500 hover:text-white hover:bg-blue-500 border border-blue-500 hover:border-blue-600 rounded transition duration-200"
					>Sign up</button>
			</div>
			<p class="mt-6 mb-4 text-sm text-center text-gray-500">
				<span>©2023 nwp-studio</span>
			</p>
		</div>
	</nav>
</aside>
