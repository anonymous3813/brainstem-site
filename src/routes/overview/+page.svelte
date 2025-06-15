<script lang="ts">
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';

	let spline;
	let scrollContainer: HTMLElement | null = null;
	let section = $state(0);
	let splineLoaded = $state(false);

	const cards = [
		{
			title: 'Welcome to the Future',
			text: 'Experience a blend of interactive 3D models and informative content, all seamlessly integrated into your browser.'
		},
		{
			title: 'Interactive 3D Environments',
			text: 'Our Spline model dynamically reacts as you scroll, revealing new perspectives and details with each section.'
		},
		{
			title: 'Contextual Information',
			text: 'Relevant details and descriptions appear alongside the visual experience, providing a rich, layered narrative.'
		},
		{
			title: 'Designed for Engagement',
			text: 'This demonstration showcases how Svelte and Spline can create truly engaging and memorable web experiences.'
		},
		{
			title: 'The Journey Continues',
			text: 'Thank you for exploring this interactive showcase. Imagine the possibilities for your next project!'
		}
	];

	onMount(() => {
		console.log('Mounting');
		if (spline) {
			spline.addEventListener('load-complete', (e) => {
				splineLoaded = true;
			});
		}

		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						section = Number(entry.target.getAttribute('data-index'));
					}
				});
			},
			{ threshold: 0.75 }
		);

		if (scrollContainer) {
			scrollContainer.querySelectorAll('.scroll-zone').forEach((el) => {
				observer.observe(el);
			});
		}

		return () => observer.disconnect();
	});
</script>

<svelte:head>
	<link
		href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap"
		rel="stylesheet"
	/>
	<script type="module" src="https://unpkg.com/@splinetool/viewer/build/spline-viewer.js"></script>
</svelte:head>

<div class="page-container">
	<div class="spline-background">
		{#if !splineLoaded}
			<div class="spline-loading-indicator" aria-label="Loading 3D model...">
				<div class="spinner"></div>
				<p>Loading 3D experience...</p>
			</div>
		{/if}
		<spline-viewer
			bind:this={spline}
			url="https://prod.spline.design/KXaFnve698K5P5iX/scene.splinecode"
			class:loaded={splineLoaded}
			onload={() => (splineLoaded = true)}
			aria-hidden={!splineLoaded}
		></spline-viewer>
		<div class="spline-blend-overlay"></div>
	</div>

	<main bind:this={scrollContainer}>
		{#each cards as card, i}
			<div
				class="scroll-zone font-sans text-white"
				data-index={i}
				aria-label={`Section ${i + 1}: ${card.title}`}
			>
				<div class="info-card-wrapper">
					{#key section}
						{#if section === i}
							<div
								in:fly={{ x: -60, opacity: 0, duration: 800, easing: quintOut }}
								out:fly={{ x: 60, opacity: 0, duration: 500 }}
								class="info-card bg-opacity-80 rounded-3xl bg-gray-800 p-8 shadow-2xl backdrop-blur-md"
							>
								<h2 class="mb-4 text-4xl font-extrabold">{card.title}</h2>
								<p class="text-xl leading-relaxed text-gray-200">{card.text}</p>
								<div class="card-accent-line"></div>
							</div>
						{/if}
					{/key}
				</div>
			</div>
		{/each}
	</main>
</div>

<style>
	:root {
		--primary-bg: #080808;
		--secondary-bg: #1a1a1a;
		--card-bg: rgba(28, 28, 30, 0.8);
		--card-border: rgba(255, 255, 255, 0.08);
		--text-color: #e0e0e0;
		--heading-color: #3b82f6;
		--accent-gradient: linear-gradient(to right, #60a5fa, #3b82f6);
		--shadow-color: rgba(0, 0, 0, 0.7);
	}

	:global(body) {
		margin: 0;
		background: var(--primary-bg);
		font-family: 'Inter', sans-serif;
		scroll-behavior: smooth;
		color: var(--text-color);
	}

	.page-container {
		display: flex;
		height: 100vh;
		width: 100vw;
		overflow: hidden;
	}

	.spline-background {
		position: relative;
		width: 50vw;
		height: 100vh;
		z-index: 1;
		overflow: hidden;
		background: radial-gradient(circle at center, var(--secondary-bg) 0%, var(--primary-bg) 100%);
		display: flex;
		align-items: center;
		justify-content: center;
	}

	spline-viewer {
		width: 100%;
		height: 100%;
		display: block;
		transform: translateZ(0);
		will-change: transform, opacity;
		opacity: 0;
		transition: opacity 1s ease-in;
	}

	spline-viewer.loaded {
		opacity: 1;
	}

	.spline-loading-indicator {
		position: absolute;
		display: flex;
		flex-direction: column;
		align-items: center;
		color: rgba(255, 255, 255, 0.6);
		font-size: 1.1rem;
		z-index: 0;
	}

	.spinner {
		border: 4px solid rgba(255, 255, 255, 0.2);
		border-top: 4px solid var(--heading-color);
		border-radius: 50%;
		width: 40px;
		height: 40px;
		animation: spin 1s linear infinite;
		margin-bottom: 10px;
	}

	@keyframes spin {
		0% {
			transform: rotate(0deg);
		}
		100% {
			transform: rotate(360deg);
		}
	}

	.spline-blend-overlay {
		position: absolute;
		top: 0;
		right: 0;
		width: 150px;
		height: 100%;
		background: linear-gradient(
			to right,
			rgba(8, 8, 8, 0) 0%,
			rgba(8, 8, 8, 0.7) 60%,
			rgba(8, 8, 8, 1) 100%
		);
		pointer-events: none;
		z-index: 2;
	}

	main {
		position: relative;
		z-index: 2;
		flex-grow: 1;
		width: 50vw;
		overflow-y: scroll;
		scroll-snap-type: y mandatory;
		background-color: transparent;
		padding-right: 2rem;
	}

	.scroll-zone {
		height: 100vh;
		scroll-snap-align: center;
		display: flex;
		align-items: center;
		justify-content: flex-start;
		padding: 0 3rem;
		position: relative;
		background-color: transparent;
	}

	.info-card-wrapper {
		display: flex;
		align-items: center;
		justify-content: flex-start;
		width: 100%;
		height: 100%;
		padding-left: 0rem;
		perspective: 1000px;
	}

	.info-card {
		width: 100%;
		max-width: 550px;
		position: relative;
		overflow: hidden;
		border: 1px solid var(--card-border);
		transform-style: preserve-3d;
		transition: transform 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
		background-color: var(--card-bg);
		box-shadow: 0 10px 30px var(--shadow-color);
	}

	.info-card:hover {
		transform: translateY(-8px) scale(1.02) translateZ(20px);
		box-shadow: 0 20px 50px var(--shadow-color);
	}

	.info-card h2 {
		text-shadow: 0px 0px 12px rgba(32, 201, 151, 0.4);
		color: var(--heading-color);
	}

	.info-card p {
		color: var(--text-color);
	}

	.card-accent-line {
		position: absolute;
		bottom: 0;
		left: 0;
		width: 100%;
		height: 5px;
		background: var(--accent-gradient);
		transform: scaleX(0);
		transform-origin: left;
		transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1);
	}

	.info-card:hover .card-accent-line {
		transform: scaleX(1);
	}
</style>
