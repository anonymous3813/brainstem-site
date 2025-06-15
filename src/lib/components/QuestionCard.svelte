<script lang="ts">
	import type { Pathway } from '$lib/types';
	const { signal, checkAnswer } = $props();
	let selectedRegion: null | string = $state(null);
</script>

<div
	class="animate-fadeIn mb-10 rounded-2xl border border-yellow-400 bg-gradient-to-br from-gray-800 via-gray-900 to-black p-6 shadow-xl"
>
	<div
		class="mb-6 text-center text-4xl font-extrabold tracking-wide text-yellow-300 drop-shadow-lg"
	>
		⚡ Signal Detected: <span class="text-white">{signal}</span>
	</div>

	<div class="grid grid-cols-1 gap-4 sm:grid-cols-3">
		{#each ['Midbrain', 'Pons', 'Medulla'] as region}
			<button
				class={`transform rounded-lg px-6 py-4 text-xl font-semibold transition-all duration-300 hover:scale-105
				${selectedRegion === region
					? 'bg-yellow-600 text-white shadow-lg ring-4 ring-yellow-300'
					: 'bg-yellow-400 text-gray-900 shadow-md hover:-translate-y-1 hover:bg-yellow-300 hover:shadow-lg focus:-translate-y-1 focus:shadow-lg focus:ring-4 focus:ring-yellow-200 focus:outline-none'
				}`}
				onclick={() => {
                    if(selectedRegion === null) {
                        checkAnswer(region);
                        selectedRegion = region;
						setTimeout(() => {
							selectedRegion = null;
						}, 5000);
                    }
				}}
			>
				{region}
			</button>
		{/each}
	</div>
</div>
