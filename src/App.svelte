<script>
  import Background from './lib/Background.svelte';
	import Application from './lib/Application.svelte'
	import Transition from './lib/Transition.svelte'
	import { _user } from './lib/data'
	import { Route, router } from 'tinro'
	// router.mode.hash()
	router.mode.memory()
	import TabBar from './lib/TabBar.svelte'
	import Start from './routes/Start.svelte'
	import Rpg from './routes/Rpg.svelte'
	import Archive from './routes/Archive.svelte'
	import Settings from './routes/Settings.svelte'
	const nav = [
		{
			name: 'Start',
			path: '/',
			icon: 'compass',
			component: Start,
			props: {
				name: 'Nwp-Home',
				header: 'Startseite',
				body: 'Are you ready for a world of fetish exploration like you never experienced before? Maskenball is here to bring you the ultimate adult playground, featuring leather, latex, crossdressing, SM games, and the chance to create your own video clips.'
			}
		},
		{
			name: 'Rpg',
			path: '/game',
			icon: 'database',
			component: Rpg,
			props: {
				name: 'Nwp-Game',
				header: 'Rpg-Game',
				body: 'Wir bieten eine Reihe perverser, fetischorientierter Aktivitäten an, darunter Crossdressing, SM-Spiele und die Möglichkeit, eigene Videoclips zu erstellen.'
			}
		},
		{
			name: 'Archiv',
			path: '/archiv',
			icon: 'archive',
			component: Archive,
			props: {
				name: 'Nwp-Archiv',
				header: 'File-Archiv',
				body: 'Ich bin jetzt seit über einem Jahr Mitglied bei Maskenball und es hat alles verändert. Ich liebe die Bandbreite an Aktivitäten, die sie anbieten, und die Community ist so einladend und unterstützend.'
			}
		},
		{
			name: 'Settings',
			path: '/settings',
			icon: 'settings',
			component: Settings,
			props: {
				name: 'Nwp-Settings',
				header: 'Settings and Options',
				body: 'Bist du bereit für eine Welt der Fetisch-Erkundung, wie du sie noch nie zuvor erlebt hast? Maskenball ist hier, um Ihnen den ultimativen Spielplatz für Erwachsene zu bieten, mit Leder, Latex, Crossdressing, SM-Spielen und der Möglichkeit, Ihre eigenen Videoclips zu erstellen.'
			}
		}
	]
</script>

<main class="main">
  <Background></Background>
	<Application let:signIn let:signOut>
		<section class="layout">
			<Transition>
				{#each nav as { path, component, props }}
					<Route {path}>
						<svelte:component this={component} {...props} />
					</Route>
				{/each}
			</Transition>
			<aside class={$router.path === '/settings' ? 'min-w-64' : ''}>
				<Route path="/settings">
					<section class="layer">
						<div class="glass">
							<div class="space-y-2 p-2">
								<h5 class="mb-0">User:</h5>
								<p>{$_user && $_user.email ? $_user.email : ''}</p>
								<button on:click={signOut} class="btn btn-blue">Logout</button>
							</div>
						</div>
					</section>
				</Route>
			</aside>
			<footer>
				<TabBar {nav} />
			</footer>
		</section>
	</Application>
</main>

<!-- 	<TabBar {nav} /> -->
