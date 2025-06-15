<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	let spline;
	const cards = [
		{ title: 'Welcome to the Future', text: 'Explore immersive web experiences.' },
		{ title: '3D + Interaction', text: 'Combine Spline and Svelte for stunning effects.' },
		{ title: 'Context-Aware Content', text: 'Content reveals as you scroll.' },
		{ title: 'Thanks for Scrolling!', text: 'This is the final card.' }
	];
</script>

<svelte:head>
	<script type="module" src="https://unpkg.com/@splinetool/viewer/build/spline-viewer.js"></script>
</svelte:head>

<section class="parallax-section">
	<div class="split-layout">
		<!-- Left: Sticky 3D Spline model -->
		<div class="spline-container">
			<spline-viewer
				bind:this={spline}
				class="spline-viewer"
				url="https://prod.spline.design/KXaFnve698K5P5iX/scene.splinecode"
			/>
		</div>

		<!-- Right: Scrollable cards -->
		<div class="card-scroll-area">
			{#each cards as card}
				<div class="scroll-card">
					<div class="card-content">
						<h2>{card.title}</h2>
						<p>{card.text}</p>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>

<style>
	.parallax-section {
		width: 100%;
		position: relative;
	}

	.split-layout {
		display: flex;
		width: 100%;
		height: 100vh;
	}

	.spline-container {
		position: sticky;
		top: 0;
		width: 50vw;
		height: 100vh;
		z-index: 0;
	}

	.spline-viewer {
		width: 100%;
		height: 100%;
		display: block;
	}

	.card-scroll-area {
		width: 50vw;
		height: 100vh;
		overflow-y: auto;
		scroll-snap-type: y mandatory;
		scroll-behavior: smooth;
		position: relative;
		z-index: 1;
	}

	.scroll-card {
		scroll-snap-align: start;
		height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 2rem;
		background-color: rgba(0, 0, 0, 0.5);
		backdrop-filter: blur(6px);
	}

	.card-content {
		max-width: 500px;
		background: rgba(15, 15, 15, 0.75);
		padding: 2rem;
		border-radius: 1rem;
		box-shadow: 0 10px 40px rgba(0, 0, 0, 0.5);
		text-align: center;
	}

	.card-content h2 {
		font-size: 2rem;
		margin-bottom: 1rem;
		color: #00ffff;
	}
	.card-content p {
		font-size: 1.25rem;
	}
</style>
