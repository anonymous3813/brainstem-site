<script lang="ts">
	import { fade } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
</script>

<svelte:head>
	<title>Brainstem Reflexes</title>
	<meta name="description" content="Learn about the brainstem's automatic reflexes that keep you alive and adapting — from heartbeat regulation to eye movements." />
	<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet" />
</svelte:head>

<div class="bg-gray-950 text-gray-100 py-16">
	<div class="container mx-auto px-4 max-w-6xl">

		<section class="text-center mb-20" in:fade={{ duration: 1000, easing: quintOut }}>
			<h1 class="text-6xl sm:text-7xl lg:text-8xl font-extrabold mb-6 leading-tight
                       text-transparent bg-clip-text bg-gradient-to-r from-teal-400 to-blue-500
                       shadow-teal-glow animate-pulse-light">
				Brainstem Reflexes
			</h1>
			<p class="text-xl md:text-2xl max-w-3xl mx-auto text-gray-300">
				Your brainstem constantly controls life-saving reflexes — without you even noticing.
			</p>
		</section>

		<section
			class="bg-gray-900 rounded-3xl p-8 md:p-12 shadow-2xl mb-16
                   transform hover:scale-[1.01] transition-transform duration-300 ease-out
                   border border-gray-700"
			in:fade={{ delay: 200, duration: 800 }}
		>
			<h2 class="text-4xl font-bold text-teal-400 mb-6 flex items-center">
				<span class="mr-3 text-5xl">🧠</span> What Are Brainstem Reflexes?
			</h2>
			<p class="text-lg md:text-xl leading-relaxed text-gray-200">
				Brainstem reflexes are automatic actions your body performs without thinking — like keeping your heart beating or making you blink when something flies toward your eyes. These reflexes help you survive and adapt to changes around you, and they’re all controlled by the brainstem.
			</p>
		</section>

		<section
			class="bg-gray-900 rounded-3xl p-8 md:p-12 shadow-2xl
                   transform hover:scale-[1.01] transition-transform duration-300 ease-out
                   border border-gray-700"
			in:fade={{ delay: 400, duration: 800 }}
		>
			<h2 class="text-4xl font-bold text-teal-400 mb-8 flex items-center">
				<span class="mr-3 text-5xl">📋</span> Key Reflexes Controlled by the Brainstem
			</h2>

			<ul class="list-disc pl-6 space-y-4 text-lg text-gray-200">
				<li>
					<strong>Cardiovascular Reflexes:</strong> Regulate your heartbeat and blood pressure.
				</li>
				<li>
					<strong>Gag Reflex:</strong> Protects your airways from choking.
				</li>
				<li>
					<strong>Swallowing Reflex:</strong> Moves food and liquids safely from your mouth to your stomach.
				</li>
				<li>
					<strong>Pupillary Light Reflex:</strong> Adjusts pupil size depending on light exposure.
				</li>
				<li>
					<strong>Vestibulo-ocular Reflex:</strong> Keeps your eyes steady when your head or body moves.
				</li>
				<li>
					<strong>Respiratory Reflexes:</strong> Regulate breathing, coughing, and sneezing.
				</li>
			</ul>
		</section>
	</div>
</div>

<style>
	.shadow-teal-glow {
		text-shadow: 0 0 15px rgba(0, 255, 255, 0.4), 0 0 30px rgba(0, 255, 255, 0.2);
	}

	@keyframes pulse-light {
		0% {
			opacity: 1;
			text-shadow: 0 0 10px rgba(0, 255, 255, 0.3), 0 0 20px rgba(0, 255, 255, 0.15);
		}
		50% {
			opacity: 0.95;
			text-shadow: 0 0 20px rgba(0, 255, 255, 0.5), 0 0 40px rgba(0, 255, 255, 0.3);
		}
		100% {
			opacity: 1;
			text-shadow: 0 0 10px rgba(0, 255, 255, 0.3), 0 0 20px rgba(0, 255, 255, 0.15);
		}
	}

	.animate-pulse-light {
		animation: pulse-light 4s infinite ease-in-out;
	}
</style>
