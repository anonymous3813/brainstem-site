<script lang="ts">
  import { fade } from 'svelte/transition';
</script>

<svelte:head>
  <title>About This Project</title>
  <meta name="description" content="Final AP Bio project combining technology and biology." />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet" />
</svelte:head>

<div class="bg-gray-900 min-h-screen flex items-center justify-center p-6 font-inter">
  <div
    class="bg-gray-800 border border-gray-700 rounded-2xl max-w-lg p-10 shadow-lg"
    in:fade={{ duration: 800 }}
  >
    <h1
      class="text-4xl font-semibold mb-6 text-center bg-gradient-to-r from-blue-400 to-teal-400 bg-clip-text text-transparent"
    >
      About This Project
    </h1>
    <p class="text-lg leading-relaxed text-gray-300 text-center">
      This is my final AP Biology project for the year. I decided on making a website since I wanted to combine technology and biology by creating an interactive web experience about the brainstem.
    </p>

    <p class="mt-10 text-right text-gray-400 italic select-none">
      — Jeffrey
    </p>
  </div>
</div>

<style>
  .font-inter {
    font-family: 'Inter', sans-serif;
  }
</style>
