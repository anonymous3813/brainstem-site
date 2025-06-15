<script lang="ts">
	import { onMount } from 'svelte';
	import brainstemData from '$lib/data/brainstem_pathways.json';
	import QuestionCard from '$lib/components/QuestionCard.svelte';
	import FeedbackCard from '$lib/components/FeedbackCard.svelte';
	import type { Pathway } from '../../lib/types';
	import GameIntroCard from '$lib/components/GameIntroCard.svelte';

	let signalNames = brainstemData.map((item) => item.signal);
	let pathways: { [signal: string]: Pathway } = {};
	brainstemData.forEach((item) => (pathways[item.signal] = item));

	let currentSignal = $state('');
	let score = $state(0);
	let feedback = $state('');
	let gameStarted = $state(false);
	let isCorrect = $state(false);
	let showInfo = $state(false);
	let selectedRegion: null | string = $state(null);

	function newSignal() {
		currentSignal = signalNames[Math.floor(Math.random() * signalNames.length)];
		selectedRegion = null;
		feedback = '';
		showInfo = false;
	}

	function startGame() {
		score = 0;
		gameStarted = true;
		newSignal();
	}

	function checkAnswer(region: string) {
		const correctRegion = pathways[currentSignal].region;
		isCorrect = region === correctRegion;
		feedback = isCorrect ? '✅ Correct!' : `❌ Wrong! It was ${correctRegion}`;
		if (isCorrect) score++;

		showInfo = true;
	}
</script>

<main class="flex min-h-screen items-center justify-center bg-black p-4 text-white">
	{#if !gameStarted}
		<GameIntroCard onclick={startGame} />
	{:else}
		<div class="w-full max-w-xl rounded-xl bg-gray-800 p-8 shadow-2xl">
			<h2
				class="user-select-none relative mb-6 inline-block rounded-full border border-yellow-400 bg-yellow-900/30 px-6 py-3 text-4xl font-extrabold text-yellow-400 backdrop-blur-sm select-none"
			>
				🏆 Score: {score}
			</h2>

			<div
				class="animate-fadeIn mb-10 rounded-2xl border border-yellow-400 bg-gradient-to-br from-gray-800 via-gray-900 to-black p-6 shadow-xl"
			>
				<div
					class="mb-6 text-center text-4xl font-extrabold tracking-wide text-yellow-300 drop-shadow-lg"
				>
					⚡ Signal Detected: <span class="text-white">{currentSignal}</span>
				</div>

				<div class="grid grid-cols-1 gap-4 sm:grid-cols-3">
					{#each ['Midbrain', 'Pons', 'Medulla'] as region}
						<button
							class={`transform rounded-lg px-6 py-4 text-xl font-semibold transition-all duration-300 hover:scale-105
				${
					selectedRegion === region
						? 'bg-yellow-600 text-white shadow-lg ring-4 ring-yellow-300'
						: 'bg-yellow-400 text-gray-900 shadow-md hover:-translate-y-1 hover:bg-yellow-300 hover:shadow-lg focus:-translate-y-1 focus:shadow-lg focus:ring-4 focus:ring-yellow-200 focus:outline-none'
				}`}
							onclick={() => {
								if (selectedRegion === null) {
									checkAnswer(region);
									selectedRegion = region;
								}
							}}
						>
							{region}
						</button>
					{/each}
				</div>
			</div>

			<FeedbackCard {feedback} {isCorrect} {showInfo} pathway={pathways[currentSignal]} />

			{#if showInfo}
				<button
					class="mt-8 w-full rounded-md bg-yellow-400 px-6 py-3 text-lg font-bold text-black shadow-md transition duration-200 hover:bg-yellow-300 active:scale-95"
					onclick={newSignal}
				>
					Continue
				</button>
			{/if}
		</div>
	{/if}
</main>
