<script >
// @ts-nocheck
	import '../app.css';
	import Coinflip from '../components/Coinflip.svelte';
	import { showCoinFlip } from '$lib/stores/coin';

	let lowHpAudio = 'paused';
</script>

<div style="width: 100%; height: 100%;">
	<Coinflip showCoinflip={$showCoinFlip} />
	<slot />
</div>

<div id="sidebar">
	<button class="sidebar-item">
		<p>Soundtrack</p>
	</button>

	<button class={`sidebar-item ${lowHpAudio === 'playing' ? 'active' : ''}`} on:click={() => {
		const audio = document.getElementById('lowhp-audio');
		if (audio && lowHpAudio !== 'playing'){
			audio.play();
			lowHpAudio = 'playing';
		} else if (audio){
			audio.pause();
			lowHpAudio = 'paused';
		}
	}}>
		<p>Low HP</p>
		<audio id="lowhp-audio" src="lowhp.mp3" preload="auto"/>
	</button>

	<button class="sidebar-item" on:click={() => {
		showCoinFlip.set(true);
	}}>
		<p>Coin flip</p>
	</button>

	<button class="sidebar-item">
		<p>Damage</p>
	</button>
</div>