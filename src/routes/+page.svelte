<script lang="ts">
	import quotes from './quotes.json';

	const angle = (Math.PI / 180) * 118;
	const vectX = Math.cos(angle);
	const vectY = Math.sin(angle);
	const shadowLength = 800;
	const shadowDensity = 1;
	const selectedIndex = Math.floor(Math.random() * quotes.length);
	let value = quotes[selectedIndex].quote;
	let author = quotes[selectedIndex].author;
	const boxShadow =
		'text-shadow:' +
		Array(shadowLength)
			.fill('')
			.map(
				(a, i) => `${(vectX * i) / shadowDensity}px ${(vectY * i) / shadowDensity}px 0px #292929`
			)
			.join(',');

	const boxShadowColored =
		'text-shadow:' +
		Array(shadowLength)
			.fill('')
			.map(
				(a, i) => `${(vectX * i) / shadowDensity}px ${(vectY * i) / shadowDensity}px 0px #342c40`
			)
			.join(',');

	let disabled = false;
	function toggleDisabled() {
		disabled = !disabled;
		const a = document.getElementsByTagName('textarea')[0];
		a.setSelectionRange(a.value.length, a.value.length);
	}
</script>

<svelte:window on:dblclick={toggleDisabled} />
<section >
	<div id="shadow1" class="shadow" style={boxShadow}>{value}</div>
	<div id="shadow2" class="shadow" style={boxShadowColored}>{value}</div>
	<textarea class="text" bind:value spellcheck="false" maxlength="128" {disabled} />
</section>

<style>
	@font-face {
		font-family: 'TTNormsPro';
		src: url('$lib/fonts/TTNormsPro-ExtraBlack.woff2');
	}
	textarea {
		position: absolute;
		text-align: left;
		border: none;
		background: none;
		outline: none;
		resize: none;
		color: white;
	}
	section {
		width: 100%;
		height: 100%;
		background: linear-gradient(248deg, #5335d7 0%, #b3a1ff 100%);
		position: relative;
		overflow: hidden;
	}

	textarea,
	.shadow {
		font-family: 'TTNormsPro', sans-serif;
		font-size: 52px;
		line-height: 0.96;
		padding: 0 0 0 10vw;
		margin: 0;
		white-space: pre-line;
		word-break: break-word;
		text-transform: uppercase;
		-webkit-font-smoothing: antialiased;
		text-align: left;
		position: absolute;
		width: 80vw;
		height: 100%;
		max-width: 1400px;
		overflow: visible;
	}

	textarea {
		border-top: 30vh solid transparent;
	}
	.shadow {
		top: 30vh;
	}

	#shadow2 {
		mask-image: url('$lib/images/circles_white.svg');
		mask-size: cover;
	}
	button{
		position: fixed;
		bottom:0;
		right:0
	}
</style>
