<script>
	const size = '40px'
	// const i1 = `<svg viewBox="0 0 80 80" fill="none" role="img" xmlns="http://www.w3.org/2000/svg" width="${size}" height="${size}"><title>Margaret Sanger</title><mask id="mask__bauhaus" maskUnits="userSpaceOnUse" x="0" y="0" width="80" height="80"><rect width="80" height="80" fill="#FFFFFF" rx="160"></rect></mask><g mask="url(#mask__bauhaus)"><rect width="80" height="80" fill="#4c264b"></rect><rect x="10" y="30" width="80" height="80" fill="#a04f62" transform="translate(-20 20) rotate(42 40 40)"></rect><circle cx="40" cy="40" fill="#d2a391" r="16" transform="translate(0 0)"></circle><line x1="0" y1="40" x2="80" y2="40" stroke-width="2" stroke="#e6d7b8" transform="translate(-4 -4) rotate(84 40 40)"></line></g></svg>`
	// const i2 = `<svg viewBox="0 0 80 80" fill="none" role="img" xmlns="http://www.w3.org/2000/svg" width="${size}" height="${size}"><title>Henrietta Swan</title><mask id="mask__bauhaus" maskUnits="userSpaceOnUse" x="0" y="0" width="80" height="80"><rect width="80" height="80" fill="#FFFFFF" rx="160"></rect></mask><g mask="url(#mask__bauhaus)"><rect width="80" height="80" fill="#a04f62"></rect><rect x="10" y="30" width="80" height="80" fill="#d2a391" transform="translate(10 10) rotate(134 40 40)"></rect><circle cx={size} cy="40" fill="#e6d7b8" r="16" transform="translate(-18 -18)"></circle><line x1="0" y1="40" x2="80" y2="40" stroke-width="2" stroke="#0e0036" transform="translate(-8 -8) rotate(268 40 40)"></line></g></svg>`
	// const i3 = `<svg viewBox="0 0 80 80" fill="none" role="img" xmlns="http://www.w3.org/2000/svg" width="${size}" height="${size}"><title>Babe Didrikson</title><mask id="mask__bauhaus" maskUnits="userSpaceOnUse" x="0" y="0" width="80" height="80"><rect width="80" height="80" fill="#FFFFFF" rx="160"></rect></mask><g mask="url(#mask__bauhaus)"><rect width="80" height="80" fill="#a04f62"></rect><rect x="10" y="30" width="80" height="80" fill="#d2a391" transform="translate(16 -16) rotate(254 40 40)"></rect><circle cx="40" cy="40" fill="#e6d7b8" r="16" transform="translate(-12 12)"></circle><line x1="0" y1="40" x2="80" y2="40" stroke-width="2" stroke="#0e0036" transform="translate(-8 8) rotate(148 40 40)"></line></g></svg>`
	// const i4 = `<svg viewBox="0 0 80 80" fill="none" role="img" xmlns="http://www.w3.org/2000/svg" width="${size}" height="${size}"><title>Patsy Takemoto</title><mask id="mask__bauhaus" maskUnits="userSpaceOnUse" x="0" y="0" width="80" height="80"><rect width="80" height="80" fill="#FFFFFF" rx="160"></rect></mask><g mask="url(#mask__bauhaus)"><rect width="80" height="80" fill="#4c264b"></rect><rect x="10" y="30" width="80" height="80" fill="#a04f62" transform="translate(-8 8) rotate(62 40 40)"></rect><circle cx="40" cy="40" fill="#d2a391" r="16" transform="translate(9 -9)"></circle><line x1="0" y1="40" x2="80" y2="40" stroke-width="2" stroke="#e6d7b8" transform="translate(-4 4) rotate(124 40 40)"></line></g></svg>`
	export let layer = 1
	export let nav = [
		{ titel: 'Generate', icon: 'generate', path: '/rpg', cn: 's1' }
	]
</script>

<section class="alpha-grid alpha-{layer}">
	{#each nav as { titel, path, icon, cn }}
		<div>
			<aside class="absolute z-10 top-4 right-4">
				<a href={path} title={titel} class="text-5xl">
					<svg class="icon rounded-full border-4 border-stone-500 icon-{icon}"
						><use xlink:href="#icon-{icon}" /></svg>
				</a>
			</aside>
			<span class="{cn} z-5" />
		</div>
	{/each}
</section>

<style>
	.alpha-0 {
		--bg0: url(./img/alpha/bg01.png);
		--bg1: url(./img/alpha/a01.png);
		--bg2: url(./img/alpha/a02.png);
		--bg3: url(./img/alpha/a03.png);
		--bg4: url(./img/alpha/a04.png);
	}
	.alpha-1 {
		--bg0: none;
		--bg1: url(./img/alpha/c01.png);
		--bg2: url(./img/alpha/c02.png);
		--bg3: url(./img/alpha/c03.png);
		--bg4: url(./img/alpha/c04.png);
		--bg-size: auto 90%;
	}
	.alpha-2 {
		--bg0: none;
		--bg1: url(./img/alpha/f01.png);
		--bg2: url(./img/alpha/f02.png);
		--bg3: url(./img/alpha/f03.png);
		--bg4: url(./img/alpha/f04.png);
		--bg-size: contain;
	}
	.alpha-grid {
		position: absolute;
		inset: 0;
		z-index: 1;
		overflow: hidden;
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-template-rows: 48% 48%;
		gap: 0px 0px;
		grid-auto-flow: row;
		grid-template-areas:
			'. .'
			'. .';
		max-width: 100%;
		height: 100%;
		background-color: transparent;
		background-image: var(--bg0);
		background-repeat: no-repeat;
		background-size: cover;
		background-position: center;
	}
	div {
		position: relative;
		overflow: hidden;
	}
	span {
		position: absolute;
		inset: 0;
		background-color: transparent;
		background-repeat: no-repeat;
		background-size: var(--bg-size, contain);
	}

	.s1 {
		background-image: var(--bg1);
		background-position: bottom right;
	}
	.s2 {
		background-image: var(--bg2);
		background-position: bottom left;
	}
	.s3 {
		background-image: var(--bg3);
		background-position: top right;
	}
	.s4 {
		background-image: var(--bg4);
		background-position: top left;
	}
	.alpha-grid-h {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr 1fr;
		grid-template-rows: 1fr;
		gap: 0px 0px;
		grid-auto-flow: row;
		grid-template-areas: '. . . .';
		width: 100%;
		height: 100%;
	}
</style>
