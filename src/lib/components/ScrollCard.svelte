<script lang="ts">
  import { fly } from 'svelte/transition';
  import { quintOut } from 'svelte/easing';

  export let card: {
    title: string;
    text: string;
    bullets?: string[];
  };
</script>

<div
  in:fly={{ x: -60, opacity: 0, duration: 800, easing: quintOut }}
  out:fly={{ x: 60, opacity: 0, duration: 500 }}
  class="group w-full max-w-[550px] relative overflow-hidden border border-white/10 transform-gpu transition duration-400 bg-[rgba(28,28,30,0.8)] shadow-[0_10px_30px_rgba(0,0,0,0.7)] rounded-3xl p-8 backdrop-blur-md hover:translate-y-[-8px] hover:scale-105 hover:shadow-[0_20px_50px_rgba(0,0,0,0.7)]"
>
  <h2 class="mb-4 text-4xl font-extrabold text-blue-500 drop-shadow-[0_0_12px_rgba(32,201,151,0.4)]">
    {card.title}
  </h2>

  <p class="text-xl leading-relaxed text-gray-200 mb-4">
    {card.text}
  </p>

  {#if card.bullets}
    <ul class="list-disc pl-5 space-y-2 text-gray-300 text-lg">
      {#each card.bullets as bullet}
        <li>{bullet}</li>
      {/each}
    </ul>
  {/if}

  <div class="absolute bottom-0 left-0 w-full h-[5px] bg-gradient-to-r from-blue-400 to-blue-600 transform scale-x-0 origin-left transition-transform duration-500 group-hover:scale-x-100"></div>
</div>
