<script lang="ts">
  import { onMount } from 'svelte';

  const text = 'Hello World';
  let display = '';
  let isDeleting = false;
  let i = 0;

  onMount(() => {
    const interval = setInterval(() => {
      if (!isDeleting) {
        display = text.slice(0, i++);
        if (i > text.length) {
          isDeleting = true;
          setTimeout(() => {}, 1000); // pause before deleting
        }
      } else {
        display = text.slice(0, --i);
        if (i === 0) isDeleting = false;
      }
    }, 100);

    return () => clearInterval(interval);
  });
</script>

<div class="flex min-h-screen items-center justify-center bg-gradient-to-tr from-indigo-900 to-blue-700 p-10">
  <div class="text-5xl font-bold text-white font-mono">
    {display}<span class="border-r-4 border-white animate-blink ml-1"></span>
  </div>
</div>

<style global>
  @keyframes blink {
    0%, 49% {
      border-color: transparent;
    }
    50%, 100% {
      border-color: white;
    }
  }

  .animate-blink {
    animation: blink 1s step-end infinite;
  }
</style>
