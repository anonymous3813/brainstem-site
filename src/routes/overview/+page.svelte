<script lang="ts">
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import cardData from '$lib/data/overview_info.json';

	let spline: HTMLElement | null = null;
	let scrollContainer: HTMLElement | null = null;
	let section = $state(0);
	let splineLoaded = $state(false);

	onMount(() => {
		if (spline) {
			spline.addEventListener('load-complete', () => {
				splineLoaded = true;
			});
		}

		const observer = new IntersectionObserver(
			(entries) => {
				for (const entry of entries) {
					if (entry.isIntersecting) {
						section = Number(entry.target.getAttribute('data-index'));
					}
				}
			},
			{ threshold: 0.75 }
		);

		if (scrollContainer) {
			scrollContainer.querySelectorAll('.scroll-zone').forEach((el) => observer.observe(el));
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

<div class="flex w-screen h-screen overflow-hidden bg-black font-inter text-white">
	<!-- Spline Viewer Side -->
	<div class="relative w-1/2 h-full flex items-center justify-center bg-gradient-radial from-neutral-900 to-black z-[1] overflow-hidden">
		{#if !splineLoaded}
			<div class="absolute flex flex-col items-center text-white/60 text-lg z-0">
				<div class="border-4 border-t-blue-500 border-white/20 rounded-full w-10 h-10 animate-spin mb-2"></div>
				<p>Loading 3D experience...</p>
			</div>
		{/if}
		<spline-viewer
			bind:this={spline}
			url="https://prod.spline.design/KXaFnve698K5P5iX/scene.splinecode"
			class:opacity-100={splineLoaded}
			class="w-full h-full transition-opacity duration-1000 opacity-0"
		></spline-viewer>
		<div class="absolute top-0 right-0 w-[150px] h-full bg-gradient-to-r from-transparent via-black/70 to-black z-20 pointer-events-none"></div>
	</div>

	<main
		bind:this={scrollContainer}
		class="relative z-[2] flex-1 w-1/2 overflow-y-scroll snap-y snap-mandatory pr-8"
	>
		{#each cardData as card, i}
			<div
				class="scroll-zone snap-center h-screen flex items-center justify-start px-12 relative"
				data-index={i}
				aria-label={`Section ${i + 1}: ${card.title}`}
			>
				<div class="flex items-center justify-start w-full h-full perspective-[1000px]">
					{#key section}
						{#if section === i}
							<div
								in:fly={{ x: -60, opacity: 0, duration: 800, easing: quintOut }}
								out:fly={{ x: 60, opacity: 0, duration: 500 }}
								class="group w-full max-w-[550px] relative overflow-hidden border border-white/10 transform-gpu transition duration-400 bg-[rgba(28,28,30,0.8)] shadow-[0_10px_30px_rgba(0,0,0,0.7)] rounded-3xl p-8 backdrop-blur-md hover:translate-y-[-8px] hover:scale-105 hover:shadow-[0_20px_50px_rgba(0,0,0,0.7)]"
							>
								<h2 class="mb-4 text-4xl font-extrabold text-blue-500 drop-shadow-[0_0_12px_rgba(32,201,151,0.4)]">{card.title}</h2>
								<p class="text-xl leading-relaxed text-gray-200">{card.text}</p>
								<div class="absolute bottom-0 left-0 w-full h-[5px] bg-gradient-to-r from-blue-400 to-blue-600 transform scale-x-0 origin-left transition-transform duration-500 group-hover:scale-x-100"></div>
							</div>
						{/if}
					{/key}
				</div>
			</div>
		{/each}
	</main>
</div>
