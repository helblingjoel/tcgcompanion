<script>
	import Modal from '../components/Modal.svelte';
	export let showCoinflip = false;

	let coinState = 'heads';
	let hasFlipped = false;

	function flipCoin() {
		coinState = 'loading';

		setTimeout(() => {
			coinState = Math.floor(Math.random() * 2) === 0 ? 'heads' : 'tails';
			hasFlipped = true;
		}, 1000)
	}
</script>

<Modal bind:showModal={showCoinflip}>
	<h2 slot="header" style="padding: 0; margin: 0;">
		Coinflip
	</h2>

	{#if hasFlipped && coinState !== 'loading'}
		<div style="width: 100%; display: grid; justify-content: center;">
			<h2 style="padding: 0; margin: 0; padding-top: 1rem;">{coinState}</h2>
		</div>
	{/if}

	<div style="width: 100%; height: 100%; display: grid; justify-content: center;">
		<button 
		id="imageWrapper"
		on:click={() => {
			flipCoin();
		}}>
		{#if coinState === 'loading'}
			<img src="loading.gif" alt="loading"/>
		{:else}
			<img src={`coin-${coinState}.png`} alt={coinState}}/>
		{/if}
		</button>

		<button style="height: 3rem;" on:click={() => {
			flipCoin();
		}}>Flip</button>
	</div>
</Modal>

<style>
	img {
		width: 25vw;
		height: 25vw;
		padding: 2rem;
	}

	#imageWrapper {
		all: unset;
	}
</style>