<script lang="ts">
	import { fade, fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
    import neurotransmitters from '$lib/data/neurotransmitters_info.json';
	
</script>

<svelte:head>
	<title>Brainstem Neurotransmitters</title>
	<meta
		name="description"
		content="Discover key neurotransmitters in the brainstem and how they affect mood, sleep, movement, and more."
	/>
</svelte:head>

<div class="bg-gray-950 py-16 text-gray-100">
	<div class="container mx-auto max-w-6xl px-4">
		<section class="mb-20 text-center" in:fade={{ duration: 1000, easing: quintOut }}>
			<h1
				class="shadow-teal-glow animate-pulse-light mb-6 bg-gradient-to-r from-blue-400 to-blue-600
					   bg-clip-text text-6xl leading-tight font-extrabold text-transparent
					   sm:text-7xl lg:text-8xl"
			>
				Brainstem Neurotransmitters
			</h1>
			<p class="mx-auto max-w-3xl text-xl text-gray-300 md:text-2xl">
				Explore the brainstem's chemical messengers that regulate your core life functions.
			</p>
		</section>

		<section class="grid grid-cols-1 gap-8 md:grid-cols-2">
			{#each neurotransmitters as nt, i}
				<div
					in:fly={{ x: i % 2 === 0 ? -40 : 40, opacity: 0, duration: 500, easing: quintOut }}
					class="group relative w-full max-w-[550px] overflow-hidden rounded-3xl border border-white/10 bg-gray-800 p-8 transition-transform duration-300 ease-out hover:scale-[1.01] hover:shadow-lg"
				>
					<h2
						class="mb-4 text-4xl font-extrabold text-blue-500 drop-shadow-[0_0_12px_rgba(32,201,151,0.4)]"
					>
						{nt.title}
					</h2>
					<p class="text-xl leading-relaxed text-gray-200">
						{nt.text}
					</p>
					<div
						class="absolute bottom-0 left-0 h-[5px] w-full origin-left scale-x-0 transform bg-gradient-to-r from-blue-400 to-blue-600 transition-transform duration-500 group-hover:scale-x-100"
					></div>
				</div>
			{/each}
		</section>
	</div>
</div>

<style>
	.shadow-teal-glow {
		text-shadow:
			0 0 15px rgba(0, 200, 255, 0.4),
			0 0 30px rgba(0, 200, 255, 0.2);
	}
	@keyframes pulse-light {
		0% {
			opacity: 1;
			text-shadow:
				0 0 10px rgba(0, 200, 255, 0.3),
				0 0 20px rgba(0, 200, 255, 0.15);
		}
		50% {
			opacity: 0.95;
			text-shadow:
				0 0 20px rgba(0, 200, 255, 0.5),
				0 0 40px rgba(0, 200, 255, 0.3);
		}
		100% {
			opacity: 1;
			text-shadow:
				0 0 10px rgba(0, 200, 255, 0.3),
				0 0 20px rgba(0, 200, 255, 0.15);
		}
	}
	.animate-pulse-light {
		animation: pulse-light 4s infinite ease-in-out;
	}
</style>
