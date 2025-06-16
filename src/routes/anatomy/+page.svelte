<script lang="ts">
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import cardData from '$lib/data/anatomy_info.json';

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

<div class="absolute top-0 left-0 z-50 h-2 w-full bg-black/50">
	<div
		class="h-full bg-gradient-to-r from-blue-400 to-blue-600 transition-all duration-300"
		style="width: {((section + 1) / cardData.length) * 100}%"
	></div>
</div>

<div class="font-inter flex h-screen w-screen overflow-hidden bg-black text-white">
	<!-- Spline Viewer Side -->
	<div
		class="bg-gradient-radial relative z-[1] flex h-full w-1/2 items-center justify-center overflow-hidden from-neutral-900 to-black"
	>
		{#if !splineLoaded}
			<div class="absolute z-0 flex flex-col items-center text-lg text-white/60">
				<div
					class="mb-2 h-10 w-10 animate-spin rounded-full border-4 border-white/20 border-t-blue-500"
				></div>
				<p>Loading 3D experience...</p>
			</div>
		{/if}
		<spline-viewer
			bind:this={spline}
			url="https://prod.spline.design/YXSZXH4iqZhXJk3q/scene.splinecode"
			class:opacity-100={splineLoaded}
			class="h-full w-full opacity-0 transition-opacity duration-1000"
		></spline-viewer>
		<div
			class="pointer-events-none absolute top-0 right-0 z-20 h-full w-[150px] bg-gradient-to-r from-transparent via-black/70 to-black"
		></div>
	</div>

	<main
		bind:this={scrollContainer}
		class="relative z-[2] w-1/2 flex-1 snap-y snap-mandatory overflow-y-scroll pr-8"
	>
		{#each cardData as card, i}
			<div
				class="scroll-zone relative flex h-screen snap-center items-center justify-start px-12"
				data-index={i}
				aria-label={`Section ${i + 1}: ${card.title}`}
			>
				<div class="flex h-full w-full items-center justify-start perspective-[1000px]">
					{#key section}
						{#if section === i}
							<div
								in:fly={{ x: -60, opacity: 0, duration: 800, easing: quintOut }}
								out:fly={{ x: 60, opacity: 0, duration: 500 }}
								class="group relative w-full max-w-[550px] transform-gpu overflow-hidden rounded-3xl border border-white/10 bg-[rgba(28,28,30,0.8)] p-8 shadow-[0_10px_30px_rgba(0,0,0,0.7)] backdrop-blur-md transition duration-400 hover:translate-y-[-8px] hover:scale-105 hover:shadow-[0_20px_50px_rgba(0,0,0,0.7)]"
							>
								<h2
									class="mb-4 text-4xl font-extrabold text-blue-500 drop-shadow-[0_0_12px_rgba(32,201,151,0.4)]"
								>
									{card.title}
								</h2>
								<p class="text-xl leading-relaxed text-gray-200">{card.text}</p>
								<div
									class="absolute bottom-0 left-0 h-[5px] w-full origin-left scale-x-0 transform bg-gradient-to-r from-blue-400 to-blue-600 transition-transform duration-500 group-hover:scale-x-100"
								></div>
							</div>
						{/if}
					{/key}
				</div>
			</div>
		{/each}
	</main>
</div>
