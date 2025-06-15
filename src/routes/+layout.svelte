<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<div class="min-h-screen flex flex-col bg-black-100 text-white">
	<!-- Header -->
	<div class="p-4 shadow-md">
		<div class="flex justify-between items-center">
			<div class="text-lg font-bold">The Brainstem</div>
			<div class="space-x-4">
				<a href="/" class="hover:text-gray-200">Home</a>
				<a href="/about" class="hover:text-gray-200">About</a>
			</div>
		</div>
	</div>

	<!-- Main Content -->
	<main class="flex-grow">
		{@render children()}
	</main>

	<!--
	<footer class="bg-gray-900 text-gray-300 py-6 mt-12">
		<div class="container mx-auto px-4 flex flex-col md:flex-row items-center justify-between gap-4 text-sm">
			<div class="text-center md:text-left">
				<p>&copy; {new Date().getFullYear()} Brainstem site</p>
			</div>
			<div class="text-center md:text-right">
				<a
					href="https://www.flaticon.com/free-icons/american-football"
					title="American football icons"
					class="text-blue-400 hover:underline"
					target="_blank"
					rel="noopener noreferrer"
				>
					Icon created by Flaticon
				</a>
			</div>
		</div>
	</footer>-->
</div>
