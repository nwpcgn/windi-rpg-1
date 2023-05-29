<script>
	import Button from '../comp/Button.svelte'
	import ButtonBar from '../comp/ButtonBar.svelte'
	const playerIcon = `<svg viewBox="0 0 90 90" fill="none" role="img" xmlns="http://www.w3.org/2000/svg" width="40" height="40"><title>Player</title><mask id="mask__ring" maskUnits="userSpaceOnUse" x="0" y="0" width="90" height="90"><rect width="90" height="90" rx="180" fill="#FFFFFF"></rect></mask><g mask="url(#mask__ring)"><path d="M83 45a38 38 0 00-76 0h76z" fill="#0ea5e9"></path><path d="M83 45a38 38 0 01-76 0h76z" fill="#0284c7"></path><path d="M0 0h90v45H0z" fill="#38bdf8"></path><path d="M0 45h90v45H0z" fill="#0ea5e9"></path><path d="M77 45a32 32 0 10-64 0h64z" fill="#0284c7"></path><path d="M77 45a32 32 0 11-64 0h64z" fill="#f4f4f4"></path><path d="M71 45a26 26 0 00-52 0h52z" fill="#f4f4f4"></path><path d="M71 45a26 26 0 01-52 0h52z" fill="#38bdf8"></path><circle cx="45" cy="45" r="23" fill="#7dd3fc"></circle></g></svg> `
	const dealerIcon = `<svg viewBox="0 0 90 90" fill="none" role="img" xmlns="http://www.w3.org/2000/svg" width="40" height="40"><title>Dealer</title><mask id="mask__ring" maskUnits="userSpaceOnUse" x="0" y="0" width="90" height="90"><rect width="90" height="90" rx="180" fill="#FFFFFF"></rect></mask><g mask="url(#mask__ring)"><path d="M0 0h90v45H0z" fill="#0284c7"></path><path d="M0 45h90v45H0z" fill="#f4f4f4"></path><path d="M83 45a38 38 0 00-76 0h76z" fill="#f4f4f4"></path><path d="M83 45a38 38 0 01-76 0h76z" fill="#7dd3fc"></path><path d="M77 45a32 32 0 10-64 0h64z" fill="#7dd3fc"></path><path d="M77 45a32 32 0 11-64 0h64z" fill="#38bdf8"></path><path d="M71 45a26 26 0 00-52 0h52z" fill="#38bdf8"></path><path d="M71 45a26 26 0 01-52 0h52z" fill="#0284c7"></path><circle cx="45" cy="45" r="23" fill="#0ea5e9"></circle></g></svg> `
	// const dealerIconB = `<svg viewBox="0 0 80 80" fill="none" role="img" xmlns="http://www.w3.org/2000/svg" width="40" height="40"><title>Dealer Bauhaus</title><mask id="mask__bauhaus" maskUnits="userSpaceOnUse" x="0" y="0" width="80" height="80"><rect width="80" height="80" rx="160" fill="#FFFFFF"></rect></mask><g mask="url(#mask__bauhaus)"><rect width="80" height="80" fill="#0ea5e9"></rect><rect x="10" y="30" width="80" height="80" fill="#0284c7" transform="translate(14 -14) rotate(36 40 40)"></rect><circle cx="40" cy="40" fill="#f4f4f4" r="16" transform="translate(3 3)"></circle><line x1="0" y1="40" x2="80" y2="40" stroke-width="2" stroke="#7dd3fc" transform="translate(12 12) rotate(72 40 40)"></line></g></svg>`
	// const playerIconB = `<svg viewBox="0 0 80 80" fill="none" role="img" xmlns="http://www.w3.org/2000/svg" width="40" height="40"><title>Player Bauhaus</title><mask id="mask__bauhaus" maskUnits="userSpaceOnUse" x="0" y="0" width="80" height="80"><rect width="80" height="80" rx="160" fill="#FFFFFF"></rect></mask><g mask="url(#mask__bauhaus)"><rect width="80" height="80" fill="#0ea5e9"></rect><rect x="10" y="30" width="80" height="10" fill="#0284c7" transform="translate(16 -16) rotate(336 40 40)"></rect><circle cx="40" cy="40" fill="#f4f4f4" r="16" transform="translate(-18 18)"></circle><line x1="0" y1="40" x2="80" y2="40" stroke-width="2" stroke="#7dd3fc" transform="translate(12 12) rotate(312 40 40)"></line></g></svg> `
	const gameDelay = 1000
	let jsbApp = {}
	// initialize letiables to track hands/cards/etc.
	jsbApp.playerHand = []
	jsbApp.dealerHand = []
	jsbApp.deck = []
	jsbApp.suitsxxx = [
		'clubs <span class="bold">&#9827</span>',
		'diamonds <span class="redcard">&#9830</span>',
		'hearts <span class="redcard">&#9829</span>',
		'spades <span class="bold">&#9824</span>'
	]
	jsbApp.suits = [
		'<span class="text-gray-700">&#9827</span>',
		'<span class="text-red-700">&#9830</span>',
		'<span class="text-red-700">&#9829</span>',
		'<span class="text-gray-700">&#9824</span>'
	]
	jsbApp.values = [
		'Ace',
		'Two',
		'Three',
		'Four',
		'Five',
		'Six',
		'Seven',
		'Eight',
		'Nine',
		'Ten',
		'Jack',
		'Queen',
		'King'
	]
	jsbApp.gameStatus = 0 // flag that game has not yet been won
	jsbApp.wins = 0 // flag that game has not yet been won
	jsbApp.draws = 0 // flag that game has not yet been won
	jsbApp.losses = 0 // flag that game has not yet been won
	jsbApp.games = 0 // flag that game has not yet been won

	let playerCardT = ``
	let dealerCardT = ``
	let playerScoreT = ``
	let dealerScoreT = ``
	let textUpdatesT = ``
	let trackerT = ``
	let showBtnBox = false
	let showNewBtn = true

	function card(suit, value, name) {
		this.suit = suit // string of c/d/h/s
		this.value = value // number 1 - 10
		this.name = name // string of the full card name
	}

	let msg = {}
	msg.p21 = 'You won! You got 21 on your initial hand!'
	msg.d21 = 'You lost! The dealer had 21 on their initial hand.'
	msg.hit = 'Hit or stay?'
	msg.stay1 = 'The dealer reveals their hidden card'
	msg.stay2 = 'Dealer hits!'
	msg.vic21 = `Your hand's value is 21!`
	msg.tracker = `<p>Wins: ${jsbApp.wins} Draws: ${jsbApp.draws} Losses: ${jsbApp.losses}</p>`
	msg.vic31 = function (dealerTotal) {
		return `Dealer busted with ${dealerTotal}!`
	}
	msg.vic41 = function (playerTotal, dealerTotal) {
		return `You had ${playerTotal} and the dealer had ${dealerTotal}.`
	}
	msg.victory = function (str) {
		return `You won!<br>${str}<br>Press 'New Game' to play again.`
	}
	msg.bust21 = function (playerTotal) {
		return `You busted with ${playerTotal}.<br>`
	}
	msg.busted = function (str) {
		return `You lost.<br>${str}Press 'New Game' to play again.`
	}
	msg.tied = function (playerTotal) {
		return `It's a tie at ${playerTotal} points each.<br>Press 'New Game' to play again.`
	}

	const newGame = function () {
		showNewBtn = false
		playerCardT = ``
		dealerCardT = ``
		jsbApp.playerHand = []
		jsbApp.dealerHand = []
		jsbApp.gameStatus = 0
		jsbApp.deck = createDeck()
		jsbApp.playerHand.push(jsbApp.deck.pop()) // Deal two cards to the player and two cards to the dealer
		jsbApp.playerHand.push(jsbApp.deck.pop())
		if (handTotal(jsbApp.playerHand) === 21) {
			jsbApp.wins += 1
			jsbApp.games += 1
			jsbApp.gameStatus = 1 // to cause the dealer's hand to be drawn face up
			drawHands()
			textUpdatesT = msg.p21
			track()
			jsbApp.gameStatus = 2 // game is won
			return
		}

		jsbApp.dealerHand.push(jsbApp.deck.pop())
		jsbApp.dealerHand.push(jsbApp.deck.pop())
		if (handTotal(jsbApp.dealerHand) === 21) {
			// check for dealer victory
			jsbApp.games += 1
			jsbApp.losses += 1
			jsbApp.gameStatus = 1 // to cause the dealer's hand to be drawn face up
			drawHands()
			textUpdatesT = msg.d21
			track()
			jsbApp.gameStatus = 2 // game is won
			return
		}

		drawHands()
		advise()
		showBtnBox = true
		textUpdatesT = 'The Initial Hands are dealt!'
	}

	const createDeck = function () {
		let deck = []
		for (let a = 0; a < jsbApp.suits.length; a++) {
			for (let b = 0; b < jsbApp.values.length; b++) {
				let cardValue = b + 1
				let cardTitle = ''
				if (cardValue > 10) {
					cardValue = 10
				}
				if (cardValue != 1) {
					if (cardValue == 11) {
						cardTitle += `${jsbApp.suits[a]} J`
					} else if (cardValue == 12) {
						cardTitle += `${jsbApp.suits[a]} Q`
					} else if (cardValue == 12) {
						cardTitle += `${jsbApp.suits[a]} K`
					} else {
						cardTitle += `${jsbApp.suits[a]} ${cardValue}`
					}
				} else {
					cardTitle += `${jsbApp.suits[a]} A`
				}
				let newCard = new card(jsbApp.suits[a], cardValue, cardTitle)
				deck.push(newCard)
			}
		}
		deck = shuffle(deck)
		jsbApp.deck = deck
		return deck
	}

	const drawHiddenT = () =>
		`<article class="p-1"><div class="bg-white text-gray-500 flex flex-col h-24 items-center justify-center rounded-md shadow-md w-24"><h1 class="text-4xl">?</h1><h2 class="text-xl"><span>?</span></h2></div></article>`
	const drawT = ({ suit, value, name }) => `
		<article class="p-1">
			<div
				class="bg-white flex flex-col h-24 items-center justify-center rounded-md shadow-md w-24">
				<h1 class="text-6xl">${suit}</h1>
				<h2 class="text-xl">${name}</h2>
			</div>
		</article>	
	`

	const drawHands = function () {
		let htmlswap = ''
		let ptotal = handTotal(jsbApp.playerHand)
		let dtotal = handTotal(jsbApp.dealerHand)
		for (let i = 0; i < jsbApp.playerHand.length; i++) {
			htmlswap += drawT(jsbApp.playerHand[i])
		}

		playerCardT = htmlswap
		playerScoreT = ptotal
		if (jsbApp.dealerHand.length == 0) {
			return
		}

		htmlswap = ''
		if (jsbApp.gameStatus === 0) {
			htmlswap += drawHiddenT()
			dealerScoreT = `${jsbApp.dealerHand[1].value} + ?`
		} else {
			dealerScoreT = dtotal
		}

		for (let i = 0; i < jsbApp.dealerHand.length; i++) {
			if (jsbApp.gameStatus === 0) {
				i += 1
			}
			htmlswap += drawT(jsbApp.dealerHand[i])
		}

		dealerCardT = htmlswap
	}

	const handTotal = function (hand) {
		let total = 0
		let aceFlag = 0 // track the number of aces in the hand
		for (let i = 0; i < hand.length; i++) {
			//console.log("Card: " + hand[i].name);
			total += hand[i].value
			if (hand[i].value == 1) {
				aceFlag += 1
			}
		}
		// For each ace in the hand, add 10 if doing so won't cause a bust
		// To show best-possible hand value
		for (let j = 0; j < aceFlag; j++) {
			if (total + 10 <= 21) {
				total += 10
			}
		}
		return total
	}

	const shuffle = function (deck) {
		let shuffledDeck = []
		let deckL = deck.length
		for (let a = 0; a < deckL; a++) {
			let randomCard = getRandomInt(0, deck.length)
			shuffledDeck.push(deck[randomCard])
			deck.splice(randomCard, 1)
		}
		return shuffledDeck
	}

	const getRandomInt = function (min, max) {
		min = Math.ceil(min)
		max = Math.floor(max)
		// console.log("Min: " + min + " Max: " + max);
		return Math.floor(Math.random() * (max - min)) + min
		// code based on sample from MDN
	}

	const deckPrinter = function (deck) {
		for (let i = 0; i < deck.length; i++) {
			console.log(deck[i].name)
		}
		return
	}

	function pressHit() {
		// disable if the game has already been won
		if (jsbApp.gameStatus === 2) {
			console.log('Hit clicked when game was over or already clicked.')
			return
		}

		// deal a card to the player and draw the hands
		jsbApp.playerHand.push(jsbApp.deck.pop())
		drawHands()

		let handVal = handTotal(jsbApp.playerHand)
		if (handVal > 21) {
			bust()
			advise()
			return
		} else if (handVal === 21) {
			victory()
			advise()
			return
		}
		advise()
		textUpdatesT = msg.hit
		return
	}

	function stayLoop() {
		if (jsbApp.gameStatus === 2) {
			console.log('Stay clicked when game was over or already clicked.')
			return
		} else if (jsbApp.gameStatus === 0) {
			// i.e. stay was just pressed
			showBtnBox = false
			let handVal = handTotal(jsbApp.dealerHand)
			jsbApp.gameStatus = 1 // enter the 'stay' loop
			advise() // clear advise
			textUpdatesT = msg.stay1
			drawHands()
			setTimeout(stayLoop, gameDelay) // return to the stay loop
		} else if (jsbApp.gameStatus === 1) {
			// If dealer has less than 17, hit
			let handVal = handTotal(jsbApp.dealerHand)
			if (handVal > 16 && handVal <= 21) {
				drawHands()
				let playerVal = handTotal(jsbApp.playerHand)
				if (playerVal > handVal) {
					victory()
					return
				} else if (playerVal < handVal) {
					bust()
					return
				} else {
					tie()
					return
				}
			}
			if (handVal > 21) {
				victory()
				return
			} // hit
			else {
				textUpdatesT = msg.stay2
				jsbApp.dealerHand.push(jsbApp.deck.pop())
				drawHands()
				setTimeout(stayLoop, gameDelay)
				return
			}
		}
	}
	function pressStay() {
		setTimeout(stayLoop, 100)
	}

	const victory = function () {
		jsbApp.wins += 1
		jsbApp.games += 1
		let explanation = ''
		jsbApp.gameStatus = 2 // flag that the game is over
		let playerTotal = handTotal(jsbApp.playerHand)
		let dealerTotal = handTotal(jsbApp.dealerHand)
		if (playerTotal === 21) {
			explanation = `Your hand's value is 21!`
		} else if (dealerTotal > 21) {
			explanation = msg.vic31(dealerTotal)
		} else {
			explanation = msg.vic41(playerTotal, dealerTotal)
		}

		textUpdatesT = msg.victory(explanation)
		track()
	}

	const bust = function () {
		jsbApp.games += 1
		jsbApp.losses += 1
		let explanation = ''
		jsbApp.gameStatus = 2 // flag that the game is over
		let playerTotal = handTotal(jsbApp.playerHand)
		let dealerTotal = handTotal(jsbApp.dealerHand)
		if (playerTotal > 21) {
			explanation = msg.bust21(playerTotal)
		}

		textUpdatesT = msg.busted(explanation)
		track()
	}

	const tie = function () {
		jsbApp.games += 1
		jsbApp.draws += 1
		let explanation = ''
		jsbApp.gameStatus = 2 // flag that the game is over
		let playerTotal = handTotal(jsbApp.playerHand)
		textUpdatesT = msg.tied(playerTotal)
		track()
	}

	const track = function () {
		trackerT = msg.tracker
		showNewBtn = true
		showBtnBox = false
	}

	// check the player hand for an ace
	const softCheck = function (hand) {
		let total = 0
		let aceFlag = 0 // track the number of aces in the hand
		for (let i = 0; i < hand.length; i++) {
			// console.log('Card: ' + hand[i].name)
			total += hand[i].value
			if (hand[i].value == 1) {
				aceFlag += 1
			}
		}
		// For each ace in the hand, add 10 if doing so won't cause a bust
		// To show best-possible hand value
		for (let j = 0; j < aceFlag; j++) {
			if (total + 10 <= 21) {
				return true // the hand is soft, i.e. it can be multiple values because of aces
			}
		}
		return false // the hand is hard, i.e. it has only one possible value
	}

	const advise = function () {
		// no advise if player has no choices
		if (jsbApp.gameStatus > 0) {
			console.log(`jsbApp.choice.innerHTML = ''`)
			return
		}
		let playerTotal = handTotal(jsbApp.playerHand)
		let soft = softCheck(jsbApp.playerHand)
		console.log('Soft: ' + soft)
		let dealerUp = jsbApp.dealerHand[1].value
		// count dealer's ace as 11 to simplify logic
		if (dealerUp === 1) {
			dealerUp = 11
		}

		// provide advice based on HIGHLY simplified blackjack basic strategy
		if (playerTotal <= 11 && !soft) {
			console.log(`jsbApp.choice.innerHTML = '[Hit!]'`)
		} else if (
			playerTotal >= 12 &&
			playerTotal <= 16 &&
			dealerUp <= 6 &&
			!soft
		) {
			console.log("jsbApp.choice.innerHTML = '[Stay]'")
		} else if (
			playerTotal >= 12 &&
			playerTotal <= 16 &&
			dealerUp >= 7 &&
			!soft
		) {
			console.log(`jsbApp.choice.innerHTML = '[Hit!]'`)
		} else if (playerTotal >= 17 && playerTotal <= 21 && !soft) {
			console.log(`jsbApp.choice.innerHTML = '[Stay]'`)
		} else if (playerTotal >= 12 && playerTotal <= 18 && soft) {
			console.log(`jsbApp.choice.innerHTML = '[Hit!]'`)
		} else if (playerTotal >= 19 && playerTotal <= 21 && soft) {
			console.log(`jsbApp.choice.innerHTML = '[Stay]'`)
		} else {
			console.log(
				`jsbApp.choice.innerHTML = 'Massive error, unexpected scenario, idk'`
			)
			console.log(
				"Error: Player's hand was " +
					playerTotal +
					" and dealer's faceup was " +
					dealerUp +
					'.'
			)
		}
		return
	}
</script>

<section class="gameboard">
	<header class="header py-4">
		<div class="max-w-xl lg:max-w-3xl mx-auto text-center">
			{#if textUpdatesT === ''}
				<h4 class="text-lg font-semibold text-blue-500 capitalize">
					Nwp-Studio
				</h4>
			{:else}
				{@html textUpdatesT}
			{/if}
		</div>
	</header>

	<article class="article flex items-center lg:flex-col lg:items-stretch">
		<section class="flex flex-col-reverse gap-1 w-full lg:flex-row">
			<div class="px-4 w-full">
				<section>
					<div class="flex items-center justify-between p-2">
						<h2
							class="flex font-bold gap-3 items-center leading-tight text-4xl">
							<span>Player</span>
							{@html playerIcon}
						</h2>
						<h4 class="text-2xl leading-tight font-medium">
							{@html playerScoreT}
						</h4>
					</div>
					<hr />
					<div class="flex flex-wrap">
						{@html playerCardT}
					</div>
				</section>
			</div>

			<div class="px-4 w-full">
				<section>
					<div class="flex items-center justify-between p-2">
						<h2
							class="flex font-bold gap-3 items-center leading-tight text-4xl">
							<span>Dealer</span>
							{@html dealerIcon}
						</h2>
						<h4 class="text-2xl leading-tight font-medium">
							{@html dealerScoreT}
						</h4>
					</div>
					<hr />
					<div class="flex flex-wrap">
						{@html dealerCardT}
					</div>
				</section>
			</div>
		</section>
	</article>
	<footer class="footer py-2">
		<div class="text-center">
			{#if showNewBtn}
				<ButtonBar>
					<Button on:click={newGame}>New Game</Button>
				</ButtonBar>
			{/if}
			{#if showBtnBox}
				<ButtonBar>
					<Button on:click={pressHit}>Hit</Button>
					<Button on:click={pressStay} color="light">Stay</Button>
				</ButtonBar>
			{/if}
		</div>
	</footer>
</section>

<style>
	.gameboard.green {
		background: radial-gradient(circle, #006600, #004d00, #003300);
		color: #f2f2f2;
	}

	.gameboard.bg-img {
		background-image: url('https://pl.sterlingcdn.com/wp-content/uploads/sites/3/2018/07/blackjack-classic-background.jpg');
		background-repeat: no-repeat;
		background-position: left top;
		background-size: auto;
	}

	.gameboard {
		position: absolute;
		bottom: 0;
		top: 0;
		right: 0;
		left: 0;
		display: grid;
		grid-template-columns: 1fr;
		grid-template-rows: minmax(80px, 100px) 2fr minmax(40px, 80px);
		grid-template-areas: 'header' 'article' 'footer';
		grid-gap: var(--game-area-gap, 0.5rem);
		padding: var(--game-area-padding, 0.5rem);
	}

	.footer {
		align-self: center;
		grid-area: footer;
	}

	.article {
		align-self: center;
		grid-area: article;
	}

	.header {
		align-self: center;
		grid-area: header;
	}
</style>
