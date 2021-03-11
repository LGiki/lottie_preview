<script>
	import lottie from "lottie-web";
	import { onMount } from 'svelte';
	let files;
	let lottiePlayer;
	let lottiePlayerElement;
	let lottiePlayerBackgroundColor = '#fff';
	onMount(() => {
		lottiePlayerElement = document.getElementById("lottie-preview");
	});

	function loadLottieAnimation(lottiePlayerElement, lottieFileUrl) {
		if (lottiePlayer) {
			lottiePlayer.destroy();
		}
		lottiePlayer = lottie.loadAnimation({
			container: lottiePlayerElement, // the dom element that will contain the animation
			renderer: "svg",
			loop: true,
			autoplay: true,
			path: lottieFileUrl, // the path to the animation json
		})
	}

	function onFileSelected() {
		if (files && files.length > 0) {
			let blobUrl = URL.createObjectURL(files[0]);
			loadLottieAnimation(lottiePlayerElement, blobUrl)
		}
	}

	function changeLottiePlayerBackgroundColor(color) {
		lottiePlayerBackgroundColor = color;
	}

</script>

<main>
	<div id="app">
		<div id="lottie-preview" style="background-color: {lottiePlayerBackgroundColor}"></div>
		<input type="file" bind:files on:change={onFileSelected} />
		<div class="operation">
			<button on:click={() => lottiePlayerBackgroundColor = '#000'}>Black</button>
			<button on:click={() => lottiePlayerBackgroundColor = '#fff'}>White</button>
			<button on:click={() => lottiePlayerBackgroundColor = 'tomato'}>Tomato</button>
			<input type="text" bind:value={lottiePlayerBackgroundColor}/>
		</div>
	</div>
</main>

<style>
	#app {
		display: flex;
		min-height: 100vh;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
</style>
