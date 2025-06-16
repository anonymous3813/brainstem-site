<script lang="ts">
	import { goto } from "$app/navigation";

	const { score, total, onRestart } = $props();
	const incorrect = total - score;
</script>

<div
	class="animate-fadeIn mx-auto max-w-xl rounded-3xl border border-blue-400 bg-gradient-to-br from-gray-800 via-gray-900 to-black p-8 text-center shadow-2xl"
>
	<h1 class="mb-4 text-5xl font-extrabold text-blue-300 drop-shadow-lg">📊 Game Summary</h1>

	<p class="mb-6 text-lg leading-relaxed tracking-wide text-gray-300">
		Here’s how you did in your brainstem journey:
	</p>

	<div class="mb-8 grid grid-cols-2 gap-6 text-2xl font-bold">
		<div class="rounded-xl border border-green-400 bg-green-800/30 py-4 text-green-300 shadow-inner">
			✅ Correct:
			<div class="mt-2 text-4xl">{score}</div>
		</div>
		<div class="rounded-xl border border-red-400 bg-red-800/30 py-4 text-red-300 shadow-inner">
			❌ Incorrect:
			<div class="mt-2 text-4xl">{incorrect}</div>
		</div>
	</div>

	<hr class="mb-8 border-t border-blue-500/30" />

	<div class="flex flex-col items-center gap-4 sm:flex-row sm:justify-center">
		<button
			class="w-full sm:w-auto transform rounded-full bg-blue-400 px-8 py-3 text-xl font-bold text-white shadow-lg transition duration-300 hover:scale-105 hover:bg-blue-300 active:scale-95"
			onclick={onRestart}
		>
			🔁 Play Again
		</button>

		<button
			class="w-full sm:w-auto transform rounded-full border border-blue-300 bg-transparent px-8 py-3 text-xl font-bold text-blue-300 shadow-lg transition duration-300 hover:scale-105 hover:bg-blue-900/40 active:scale-95"
			onclick={() => goto("/")}
		>
			Return Home
		</button>
	</div>
</div>
