<script lang="ts"> 
	import { onMount } from 'svelte';
	import brainstemData from '$lib/data/brainstem_pathways.json';
	import FeedbackCard from '$lib/components/FeedbackCard.svelte';
	import GameIntroCard from '$lib/components/GameIntroCard.svelte';
	import GameSummaryCard from '$lib/components/GameSummaryCard.svelte';
	import type { Pathway } from '../../lib/types';

	const startingTime = 60;

	let signalNames = brainstemData.map((item) => item.signal);
	let pathways: { [signal: string]: Pathway } = {};
	brainstemData.forEach((item) => (pathways[item.signal] = item));

	let currentSignal = $state('');
	let score = $state(0);
	let feedback = $state('');
	let gameStarted = $state(false);
	let gameOver = $state(false);
	let isCorrect = $state(false);
	let showInfo = $state(false);
	let selectedRegion: null | string = $state(null);
	let questionCount = $state(0);

	let timeLeft = $state(startingTime);
	let timer: ReturnType<typeof setInterval> | null = null;

	function newSignal() {
		if (questionCount >= signalNames.length) {
			endGame();
			return;
		}
		currentSignal = signalNames[Math.floor(Math.random() * signalNames.length)];
		selectedRegion = null;
		feedback = '';
		showInfo = false;
	}

	function startGame() {
		score = 0;
		questionCount = 0;
		timeLeft = startingTime;
		gameStarted = true;
		gameOver = false;
		newSignal();

		if (timer) clearInterval(timer);
		timer = setInterval(() => {
			timeLeft--;
			if (timeLeft <= 0) {
				endGame();
			}
		}, 1000);
	}

	function endGame() {
		gameStarted = false;
		gameOver = true;
		if (timer) {
			clearInterval(timer);
			timer = null;
		}
	}

	function checkAnswer(region: string) {
		const correctRegion = pathways[currentSignal].region;
		isCorrect = region === correctRegion;
		feedback = isCorrect ? '✅ Correct!' : `❌ Wrong! It was ${correctRegion}`;
		questionCount++;
		if (isCorrect) score++;
		showInfo = true;
	}
</script>

<main class="flex min-h-screen items-center justify-center bg-black p-4 text-white">
	{#if gameOver}
		<!-- Summary screen -->
		<GameSummaryCard 
			score={score}
			total={questionCount}
			onRestart={startGame}
		/>
	{:else if !gameStarted}
		<GameIntroCard onclick={startGame} />
	{:else}
		<div
			class="w-full max-w-xl rounded-xl border border-blue-400 bg-gradient-to-br from-gray-800 via-gray-900 to-black p-8 shadow-2xl"
		>
			<!-- Score and Timer Row -->
			<div class="flex items-center justify-between mb-6">
				<h2 class="rounded-full border border-blue-400 bg-blue-900/30 px-6 py-3 text-2xl font-extrabold text-blue-400 backdrop-blur-sm">
					🏆 Score: {score}
				</h2>
				<div
					class="rounded-full border border-cyan-400 bg-cyan-900/30 px-6 py-3 text-xl font-bold text-cyan-300 animate-pulse backdrop-blur-sm"
				>
					⏳ {timeLeft}s
				</div>
			</div>

			<div
				class="animate-fadeIn mb-10 rounded-2xl border border-blue-400 bg-gradient-to-br from-gray-800 via-gray-900 to-black p-6 shadow-xl"
			>
				<div
					class="mb-6 text-center text-4xl font-extrabold tracking-wide text-blue-300 drop-shadow-lg"
				>
					⚡ Signal Detected: <span class="text-white">{currentSignal}</span>
				</div>

				<div class="grid grid-cols-1 gap-4 sm:grid-cols-3">
					{#each ['Midbrain', 'Pons', 'Medulla'] as region}
						<button
							class={`transform rounded-lg px-6 py-4 text-xl font-semibold transition-all duration-300 hover:scale-105
								${
									selectedRegion === region
										? 'bg-blue-600 text-white shadow-lg ring-4 ring-blue-300'
										: 'bg-blue-400 text-white shadow-md hover:-translate-y-1 hover:bg-blue-300 hover:shadow-lg focus:-translate-y-1 focus:shadow-lg focus:ring-4 focus:ring-blue-200 focus:outline-none'
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
				<div class="mt-8 flex flex-col gap-4 sm:flex-row sm:justify-between">
					<button
						class="w-full rounded-md bg-blue-400 px-6 py-3 text-lg font-bold text-white shadow-md transition duration-200 hover:bg-blue-300 active:scale-95"
						onclick={newSignal}
					>
						Continue
					</button>
					<button
						class="w-full rounded-md border border-blue-300 bg-transparent px-6 py-3 text-lg font-bold text-blue-300 shadow-md transition duration-200 hover:bg-blue-900/40 active:scale-95"
						onclick={endGame}
					>
						Quit Game
					</button>
				</div>
			{/if}
		</div>
	{/if}
</main>
