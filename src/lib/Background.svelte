<script>
	import { onMount } from 'svelte'
	let op1 = false
	let maxWidth = 1000
	let maxHeight = 680
	let ratio = 0
	let width = 576
	let height = 324
	let ratio2 = 0
	let width2 = 1200
	let height2 = 675

	const resizeImg = () => {
		// if (width > maxWidth) {
		// 	ratio = maxWidth / width // get ratio for scaling image
		// 	// $(this).css('width', maxWidth) // Set new width
		// 	// $(this).css('height', height * ratio) // Scale height based on ratio
		// 	height = height * ratio // Reset height to match scaled image
		// 	width = width * ratio // Reset width to match scaled image
		// }
		// Check if current height is larger than max
		if (height > maxHeight) {
			ratio = maxHeight / height // get ratio for scaling image
			// $(this).css('height', maxHeight) // Set new height
			// $(this).css('width', width * ratio) // Scale width based on ratio
			width = width * ratio // Reset width to match scaled image
			height = height * ratio // Reset height to match scaled image
		}

		if (height <= maxHeight) {
			ratio = maxHeight / height
			width = width * ratio
			height = maxHeight
		}

		if (height2 >= maxHeight) {
			ratio2 = maxHeight / height2
			width2 = width2 * ratio
			height2 = maxHeight
		} else {
			ratio2 = maxHeight / height2
			width2 = width2 * ratio
			height2 = maxHeight
		}
	}
	const setImg = () => {
		width = 576
		height = 324
	}

	onMount(() => {
		setImg()
		resizeImg()
	})

	$: style = `--cv-width: ${
		width * 3
	}px; --cv-height: ${height}px; --img-width: -${width}px;`

	$: style2 = `--cv-width: ${
		width2 * 3
	}px; --cv-height: ${height2}px; --img-width: -${width2}px;`
</script>

<div
	class="bg-wrapper"
	bind:clientWidth={maxWidth}
	bind:clientHeight={maxHeight}>
	{#if op1}
		<div class="animate bg1" {style} />
		<div class="animate bg2" {style} />
		<div class="animate bg3" {style} />
	{:else}
		<div class="static bg11" style={style2} />
	{/if}
</div>

<style>
	.bg-wrapper {
		position: absolute;
		inset: 0;
		z-index: -10;
		overflow: hidden;
	}
	.static {
		--bg: url('./img/bg1/6.png');
		position: absolute;
		inset: 0;
		background: var(--bg) repeat-x left top;
		background-size: auto 100%;
	}
	.animate {
		position: absolute;
		left: 0;
		top: 0;
		height: var(--cv-height);
		width: var(--cv-width);
		background-image: var(--bg);
		background-size: contain;
		background-repeat: repeat-x;
		animation-name: slide;
		animation-duration: var(--ani-d);
		animation-timing-function: linear;
		animation-iteration-count: infinite;
	}
	.bg1 {
		--bg: url('./img/bg1/1.png');
		animation: none;
	}
	.bg2 {
		--bg: url('./img/bg1/3.png'), url('./img/bg1/2.png');
		--ani-d: 30s;
	}
	.bg3 {
		--bg: url('./img/bg1/5.png'), url('./img/bg1/4.png');
		--ani-d: 28s;
	}
	.animate2 {
		position: absolute;
		left: 0;
		top: 0;
		height: var(--cv-height);
		width: var(--cv-width);
		background-image: var(--bg);
		background-size: contain;
		background-repeat: repeat-x;
		animation-name: slide;
		animation-duration: var(--ani-d);
		animation-timing-function: linear;
		animation-iteration-count: infinite;
	}
	.bg11 {
		--bg: url('./img/bg2/bg1.png');
		--ani-d: 30s;
	}

	@keyframes slide {
		0% {
			transform: translate3d(0, 0, 0);
		}
		100% {
			transform: translate3d(var(--img-width), 0, 0); /* The image width */
		}
	}
</style>
