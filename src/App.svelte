<script>
	import BlackJack from './bj/BlackJack.svelte'
	import Button from './lib/Button.svelte'
	import Rpg from './routes/Start.svelte'
	import Settings from './views/Settings.svelte'
	import Sidebar from './lib/Sidebar.svelte'
	import TopAppBar from './lib/TopAppBar.svelte'
	import { Route, router } from 'tinro'
	router.mode.memory()
	let open = false
	let open2 = false
	let alphaLayer = 1
</script>

<Sidebar bind:open />

<Settings bind:open={open2} bind:alphaLayer />

<TopAppBar bind:open bind:open2 />

<Route path="/">
	<main class="main">
		<section class="py-12">
			<div class="container px-4 mx-auto">
				<div class="max-w-xl lg:max-w-3xl mx-auto text-center">
					<span class="text-xs font-semibold text-blue-500 uppercase"
						>Nwp-Studio</span>
					<h2
						class="mt-2 mb-4 text-3xl leading-tight md:text-4xl md:leading-tight lg:text-5xl lg:leading-tight font-bold font-heading">
						Willkommen bei Maskenball!
					</h2>
					<p
						class="mb-8 text-base leading-relaxed lg:text-xl lg:leading-relaxed text-gray-500">
						Lack, Leder, Latex, Crossdressing, SM-Spiele und eigene Videoclips
						erstellen
					</p>

					<div class="flex justify-center gap-1">
						<Button href="/bj">Start Game</Button>
						<Button href="/info">Alpha Grid</Button>
						<Button color="light" on:click={() => (open2 = true)}
							>Information</Button>
					</div>
				</div>
			</div>
		</section>
	</main>
</Route>
<Route path="/bj">
	<main class="main">
		<BlackJack />
	</main>
</Route>
<Route path="/rpg/*">

		<Rpg bind:alphaLayer />
	
</Route>


<!-- prettier-ignore -->
<svg
	aria-hidden="true"
	style="position: absolute; width: 0; height: 0; overflow: hidden;"
	version="1.1"
	xmlns="http://www.w3.org/2000/svg"
	xmlns:xlink="http://www.w3.org/1999/xlink">
	<defs>
		<symbol id="icon-wood" viewBox="0 0 90 90" fill="none"><title>Wood</title><mask id="mask__ring" maskUnits="userSpaceOnUse" x="0" y="0" width="90" height="90"><rect width="90" height="90" rx="180" fill="#FFFFFF"></rect></mask><g mask="url(#mask__ring)"><path d="M0 0h90v45H0z" fill="#ffeccb"></path><path d="M0 45h90v45H0z" fill="#c9031a"></path><path d="M83 45a38 38 0 00-76 0h76z" fill="#c9031a"></path><path d="M83 45a38 38 0 01-76 0h76z" fill="#9d1722"></path><path d="M77 45a32 32 0 10-64 0h64z" fill="#9d1722"></path><path d="M77 45a32 32 0 11-64 0h64z" fill="#4a2723"></path><path d="M71 45a26 26 0 00-52 0h52z" fill="#4a2723"></path><path d="M71 45a26 26 0 01-52 0h52z" fill="#ffeccb"></path><circle cx="45" cy="45" r="23" fill="#07a2a6"></circle></g></symbol>
		<symbol id="icon-iron" viewBox="0 0 90 90" fill="none"><title>Iron</title><mask id="mask__ring" maskUnits="userSpaceOnUse" x="0" y="0" width="90" height="90"><rect width="90" height="90" rx="180" fill="#FFFFFF"></rect></mask><g mask="url(#mask__ring)"><path d="M0 0h90v45H0z" fill="#07a2a6"></path><path d="M0 45h90v45H0z" fill="#ffeccb"></path><path d="M83 45a38 38 0 00-76 0h76z" fill="#ffeccb"></path><path d="M83 45a38 38 0 01-76 0h76z" fill="#c9031a"></path><path d="M77 45a32 32 0 10-64 0h64z" fill="#c9031a"></path><path d="M77 45a32 32 0 11-64 0h64z" fill="#9d1722"></path><path d="M71 45a26 26 0 00-52 0h52z" fill="#9d1722"></path><path d="M71 45a26 26 0 01-52 0h52z" fill="#07a2a6"></path><circle cx="45" cy="45" r="23" fill="#4a2723"></circle></g></symbol>
		<symbol id="icon-stone" viewBox="0 0 90 90" fill="none"><title>Stone</title><mask id="mask__ring" maskUnits="userSpaceOnUse" x="0" y="0" width="90" height="90"><rect width="90" height="90" rx="180" fill="#FFFFFF"></rect></mask><g mask="url(#mask__ring)"><path d="M0 0h90v45H0z" fill="#9d1722"></path><path d="M0 45h90v45H0z" fill="#4a2723"></path><path d="M83 45a38 38 0 00-76 0h76z" fill="#4a2723"></path><path d="M83 45a38 38 0 01-76 0h76z" fill="#07a2a6"></path><path d="M77 45a32 32 0 10-64 0h64z" fill="#07a2a6"></path><path d="M77 45a32 32 0 11-64 0h64z" fill="#ffeccb"></path><path d="M71 45a26 26 0 00-52 0h52z" fill="#ffeccb"></path><path d="M71 45a26 26 0 01-52 0h52z" fill="#9d1722"></path><circle cx="45" cy="45" r="23" fill="#c9031a"></circle></g></symbol>
		<symbol id="icon-food" viewBox="0 0 90 90" fill="none"><title>Food</title><mask id="mask__ring" maskUnits="userSpaceOnUse" x="0" y="0" width="90" height="90"><rect width="90" height="90" rx="180" fill="#FFFFFF"></rect></mask><g mask="url(#mask__ring)"><path d="M0 0h90v45H0z" fill="#4a2723"></path><path d="M0 45h90v45H0z" fill="#07a2a6"></path><path d="M83 45a38 38 0 00-76 0h76z" fill="#07a2a6"></path><path d="M83 45a38 38 0 01-76 0h76z" fill="#ffeccb"></path><path d="M77 45a32 32 0 10-64 0h64z" fill="#ffeccb"></path><path d="M77 45a32 32 0 11-64 0h64z" fill="#c9031a"></path><path d="M71 45a26 26 0 00-52 0h52z" fill="#c9031a"></path><path d="M71 45a26 26 0 01-52 0h52z" fill="#4a2723"></path><circle cx="45" cy="45" r="23" fill="#9d1722"></circle></g></symbol>
		<symbol id="icon-build" viewBox="0 0 80 80" fill="none"><title>Build</title><mask id="mask__bauhaus" maskUnits="userSpaceOnUse" x="0" y="0" width="80" height="80"><rect width="80" height="80" rx="160" fill="#FFFFFF"></rect></mask><g mask="url(#mask__bauhaus)"><rect width="80" height="80" fill="#9d1722"></rect><rect x="10" y="30" width="80" height="80" fill="#4a2723" transform="translate(12 12) rotate(92 40 40)"></rect><circle cx="40" cy="40" fill="#07a2a6" r="16" transform="translate(12 -12)"></circle><line x1="0" y1="40" x2="80" y2="40" stroke-width="2" stroke="#ffeccb" transform="translate(-4 4) rotate(184 40 40)"></line></g></symbol>
		<symbol id="icon-store" viewBox="0 0 80 80" fill="none"><title>Store</title><mask id="mask__bauhaus" maskUnits="userSpaceOnUse" x="0" y="0" width="80" height="80"><rect width="80" height="80" rx="160" fill="#FFFFFF"></rect></mask><g mask="url(#mask__bauhaus)"><rect width="80" height="80" fill="#c9031a"></rect><rect x="10" y="30" width="80" height="10" fill="#9d1722" transform="translate(4 -4) rotate(90 40 40)"></rect><circle cx="40" cy="40" fill="#4a2723" r="16" transform="translate(18 18)"></circle><line x1="0" y1="40" x2="80" y2="40" stroke-width="2" stroke="#07a2a6" transform="translate(0 0) rotate(180 40 40)"></line></g></symbol>
		<symbol id="icon-worker" viewBox="0 0 80 80" fill="none"><title>Worker</title><mask id="mask__bauhaus" maskUnits="userSpaceOnUse" x="0" y="0" width="80" height="80"><rect width="80" height="80" rx="160" fill="#FFFFFF"></rect></mask><g mask="url(#mask__bauhaus)"><rect width="80" height="80" fill="#4a2723"></rect><rect x="10" y="30" width="80" height="80" fill="#07a2a6" transform="translate(0 0) rotate(324 40 40)"></rect><circle cx="40" cy="40" fill="#ffeccb" r="16" transform="translate(-3 -3)"></circle><line x1="0" y1="40" x2="80" y2="40" stroke-width="2" stroke="#c9031a" transform="translate(-8 8) rotate(288 40 40)"></line></g></symbol>
		<symbol id="icon-generate" viewBox="0 0 80 80" fill="none"><title>Generate</title><mask id="mask__bauhaus" maskUnits="userSpaceOnUse" x="0" y="0" width="80" height="80"><rect width="80" height="80" rx="160" fill="#FFFFFF"></rect></mask><g mask="url(#mask__bauhaus)"><rect width="80" height="80" fill="#c9031a"></rect><rect x="10" y="30" width="80" height="80" fill="#9d1722" transform="translate(16 16) rotate(10 40 40)"></rect><circle cx="40" cy="40" fill="#4a2723" r="16" transform="translate(15 -15)"></circle><line x1="0" y1="40" x2="80" y2="40" stroke-width="2" stroke="#07a2a6" transform="translate(0 0) rotate(20 40 40)"></line></g></symbol>
		<symbol id="icon-population2" viewBox="0 0 90 90" fill="none"><title>Population</title><mask id="mask__ring" maskUnits="userSpaceOnUse" x="0" y="0" width="90" height="90"><rect width="90" height="90" rx="180" fill="#FFFFFF"></rect></mask><g mask="url(#mask__ring)"><path d="M0 0h90v45H0z" fill="#ffeccb"></path><path d="M0 45h90v45H0z" fill="#c9031a"></path><path d="M83 45a38 38 0 00-76 0h76z" fill="#c9031a"></path><path d="M83 45a38 38 0 01-76 0h76z" fill="#9d1722"></path><path d="M77 45a32 32 0 10-64 0h64z" fill="#9d1722"></path><path d="M77 45a32 32 0 11-64 0h64z" fill="#4a2723"></path><path d="M71 45a26 26 0 00-52 0h52z" fill="#4a2723"></path><path d="M71 45a26 26 0 01-52 0h52z" fill="#ffeccb"></path><circle cx="45" cy="45" r="23" fill="#07a2a6"></circle></g></symbol>
		<symbol id="icon-population" viewBox="0 0 36 36" fill="none"><title>Population</title><mask id="mask__beam" maskUnits="userSpaceOnUse" x="0" y="0" width="36" height="36"><rect width="36" height="36" rx="72" fill="#FFFFFF"></rect></mask><g mask="url(#mask__beam)"><rect width="36" height="36" fill="#4a2723"></rect><rect x="0" y="0" width="36" height="36" transform="translate(9 -5) rotate(339 18 18) scale(1)" fill="#ffeccb" rx="6"></rect><g transform="translate(4.5 -4) rotate(9 18 18)"><path d="M15 19c2 1 4 1 6 0" stroke="#000000" fill="none" stroke-linecap="round"></path><rect x="10" y="14" width="1.5" height="2" rx="1" stroke="none" fill="#000000"></rect><rect x="24" y="14" width="1.5" height="2" rx="1" stroke="none" fill="#000000"></rect></g></g></symbol>
		<symbol id="icon-maxpop2" viewBox="0 0 90 90" fill="none"><title>Maxpop</title><mask id="mask__ring" maskUnits="userSpaceOnUse" x="0" y="0" width="90" height="90"><rect width="90" height="90" rx="180" fill="#FFFFFF"></rect></mask><g mask="url(#mask__ring)"><path d="M0 0h90v45H0z" fill="#4a2723"></path><path d="M0 45h90v45H0z" fill="#07a2a6"></path><path d="M83 45a38 38 0 00-76 0h76z" fill="#07a2a6"></path><path d="M83 45a38 38 0 01-76 0h76z" fill="#ffeccb"></path><path d="M77 45a32 32 0 10-64 0h64z" fill="#ffeccb"></path><path d="M77 45a32 32 0 11-64 0h64z" fill="#c9031a"></path><path d="M71 45a26 26 0 00-52 0h52z" fill="#c9031a"></path><path d="M71 45a26 26 0 01-52 0h52z" fill="#4a2723"></path><circle cx="45" cy="45" r="23" fill="#9d1722"></circle></g></symbol>
		<symbol id="icon-maxpop" viewBox="0 0 36 36" fill="none"><title>Maxpop</title><mask id="mask__beam" maskUnits="userSpaceOnUse" x="0" y="0" width="36" height="36"><rect width="36" height="36" rx="72" fill="#FFFFFF"></rect></mask><g mask="url(#mask__beam)"><rect width="36" height="36" fill="#c9031a"></rect><rect x="0" y="0" width="36" height="36" transform="translate(-3 -3) rotate(227 18 18) scale(1.2)" fill="#4a2723" rx="36"></rect><g transform="translate(-3 -5) rotate(7 18 18)"><path d="M15 21c2 1 4 1 6 0" stroke="#FFFFFF" fill="none" stroke-linecap="round"></path><rect x="12" y="14" width="1.5" height="2" rx="1" stroke="none" fill="#FFFFFF"></rect><rect x="22" y="14" width="1.5" height="2" rx="1" stroke="none" fill="#FFFFFF"></rect></g></g></symbol>
		<symbol id="icon-info" viewBox="0 0 24 24"><title>info</title><path d="M12 20.016q3.281 0 5.648-2.367t2.367-5.648-2.367-5.648-5.648-2.367-5.648 2.367-2.367 5.648 2.367 5.648 5.648 2.367zM12 2.016q4.125 0 7.055 2.93t2.93 7.055-2.93 7.055-7.055 2.93-7.055-2.93-2.93-7.055 2.93-7.055 7.055-2.93zM11.016 6.984h1.969v6h-1.969v-6zM11.016 15h1.969v2.016h-1.969v-2.016z"></path></symbol>
		<symbol id="icon-close" viewbox="0 0 24 24"><title>close</title><path d="M18.984 6.422l-5.578 5.578 5.578 5.578-1.406 1.406-5.578-5.578-5.578 5.578-1.406-1.406 5.578-5.578-5.578-5.578 1.406-1.406 5.578 5.578 5.578-5.578z"></path></symbol>
		<symbol id="icon-error" viewbox="0 0 24 24"><title>error</title><path d="M17.016 15.609l-3.609-3.609 3.609-3.609-1.406-1.406-3.609 3.609-3.609-3.609-1.406 1.406 3.609 3.609-3.609 3.609 1.406 1.406 3.609-3.609 3.609 3.609zM12 2.016q4.125 0 7.055 2.93t2.93 7.055-2.93 7.055-7.055 2.93-7.055-2.93-2.93-7.055 2.93-7.055 7.055-2.93z"></path></symbol>
		<symbol id="icon-success" viewbox="0 0 24 24"><title>success</title><path d="M9 16.172l10.594-10.594 1.406 1.406-12 12-5.578-5.578 1.406-1.406z"></path></symbol>
	</defs>
</svg>
