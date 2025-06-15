<script>
	const { onclick } = $props();
</script>

<div
	class="animate-fadeIn mx-auto max-w-xl rounded-3xl border border-yellow-400 bg-gradient-to-br from-gray-800 via-gray-900 to-black p-8 text-center shadow-2xl"
>
	<h1 class="mb-4 text-6xl font-extrabold text-yellow-300 drop-shadow-lg">🧠 Nerve Relay</h1>
	<p class="mb-6 text-lg leading-relaxed tracking-wide text-gray-300">
		You're a neural signal, traveling through the brainstem.<br />
		Can you choose the right path and keep the body functioning?
	</p>
	<div class="mb-6 flex justify-center">
		<span class="animate-pulse text-4xl text-blue-400">⚡</span>
		<span class="mx-2 animate-pulse text-4xl text-green-400">⚡</span>
		<span class="animate-pulse text-4xl text-pink-400">⚡</span>
	</div>
	<button
		class="button transform rounded-full bg-yellow-400 px-8 py-3 text-2xl font-bold text-black shadow-lg transition duration-300 ease-in-out hover:scale-105 hover:bg-yellow-300"
		{onclick}
	>
		Start Journey
	</button>
</div>
