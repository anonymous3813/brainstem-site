<script lang="ts">
	import type { Pathway } from '$lib/types';
	const { feedback, isCorrect, showInfo, pathway } = $props();
</script>

{#if feedback}
	<div
		class={`text-3xl font-extrabold my-6 px-6 py-4 rounded-xl shadow-lg transition-all duration-500 ${
			isCorrect
				? 'bg-green-600 text-white border-2 border-green-300 animate-bounce-in'
				: 'bg-red-600 text-white border-2 border-red-300 animate-shake'
		}`}
	>
		{feedback}
	</div>
{/if}

{#if showInfo && pathway}
	<div
		class="bg-gradient-to-br from-gray-800 via-gray-900 to-black rounded-2xl p-6 mt-6 text-left shadow-xl border border-yellow-500 animate-fadeIn"
	>
		<h3 class="text-2xl font-bold text-yellow-300 mb-3">🧠 Deep Dive</h3>
		<p class="text-base text-gray-100 mb-4 leading-relaxed">{pathway.description}</p>

		{#if pathway.cranialNerves?.length}
			<p class="text-sm text-blue-300 mb-1">
				<strong>Cranial Nerves:</strong> {pathway.cranialNerves.join(', ')}
			</p>
		{/if}
		{#if pathway.relatedConditions?.length}
			<p class="text-sm text-pink-300">
				<strong>Related Conditions:</strong> {pathway.relatedConditions.join(', ')}
			</p>
		{/if}
	</div>
{/if}

<style>
    @keyframes bounce-in {
	0% {
		transform: scale(0.9);
		opacity: 0;
	}
	60% {
		transform: scale(1.05);
		opacity: 1;
	}
	100% {
		transform: scale(1);
	}
}

.animate-bounce-in {
	animation: bounce-in 0.6s ease-out;
}

@keyframes shake {
	0%, 100% { transform: translateX(0); }
	25% { transform: translateX(-5px); }
	50% { transform: translateX(5px); }
	75% { transform: translateX(-5px); }
}

.animate-shake {
	animation: shake 0.4s ease-in-out;
}

@keyframes fadeIn {
	from {
		opacity: 0;
		transform: translateY(10px);
	}
	to {
		opacity: 1;
		transform: translateY(0);
	}
}

.animate-fadeIn {
	animation: fadeIn 0.4s ease-out;
}

</style>