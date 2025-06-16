<script lang="ts">
	import { onMount } from 'svelte';

	let base = "The brainstem controls";
	let phrases = [
		"breathing.",
		"your heartbeat.",
		"reflexes.",
		"your sleep cycle.",
		"movement and balance."
	];
	let currentPhraseIndex = 0;
	let displayedText = '';
	let fullText = '';
	let isDeleting = false;
	let typingSpeed = 75;
	let delayBetweenPhrases = 1500;
	let showCursor = true;

	function type() {
		fullText = phrases[currentPhraseIndex];

		if (isDeleting) {
			displayedText = fullText.substring(0, displayedText.length - 1);
		} else {
			displayedText = fullText.substring(0, displayedText.length + 1);
		}

		if (!isDeleting && displayedText === fullText) {
			setTimeout(() => {
				isDeleting = true;
				type();
			}, delayBetweenPhrases);
			return;
		} else if (isDeleting && displayedText === '') {
			isDeleting = false;
			currentPhraseIndex = (currentPhraseIndex + 1) % phrases.length;
		}

		setTimeout(type, isDeleting ? 30 : typingSpeed);
	}

	onMount(() => {
		type();
		setInterval(() => {
			showCursor = !showCursor;
		}, 500);
	});
</script>

<div class="min-h-screen bg-gradient-to-br from-gray-900 via-black to-blue-950 text-white flex flex-col items-center justify-center p-6">
	<h1 class="text-5xl md:text-7xl font-extrabold bg-gradient-to-r from-blue-400 via-sky-300 to-cyan-200 text-transparent bg-clip-text mb-6 text-center">
		The Brainstem Project
	</h1>

	<p class="text-lg md:text-xl text-blue-200 mb-8 text-center max-w-xl">
		Exploring the vital core of your nervous system.
	</p>

	<h2 class="text-xl md:text-2xl text-blue-200 mb-2">{base}</h2>

	<!-- Typewriter area -->
	<div class="bg-zinc-900 text-blue-300 text-2xl md:text-3xl font-mono px-6 py-3 rounded-md border border-blue-500 shadow-md inline-flex items-center justify-center min-w-[300px]">
		<span>{displayedText}</span>
		<span
			class="ml-1 w-[1px] h-[1.25em] bg-blue-400 animate-blink"
			class:opacity-0={!showCursor}
		></span>
	</div>

	<!-- Navigation links -->
	<div class="mt-12 flex flex-wrap gap-4 justify-center">
		{#each [
			{ href: "/overview", label: "Overview" },
			{ href: "/anatomy", label: "Anatomy" },
			{ href: "/reflexes", label: "Reflexes" },
			{ href: "/neurotransmitters", label: "Neurotransmitters" },
			//{ href: "/cranial-nerves", label: "Cranial Nerves" }
			{ href: "/nerve-relay", label: "Nerve Relay" }
		] as item}
			<a
				href={item.href}
				class="px-5 py-2 rounded-full border border-blue-400 text-blue-300 hover:bg-blue-600 hover:text-white transition">
				{item.label}
			</a>
		{/each}
	</div>
</div>

<style>
	@keyframes blink {
		0%, 100% { opacity: 1; }
		50% { opacity: 0; }
	}
	.animate-blink {
		animation: blink 1s steps(2, start) infinite;
	}
</style>
