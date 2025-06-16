<script lang="ts">
    import { fly } from 'svelte/transition';
    import { quintOut } from 'svelte/easing';

    const cardData = [
        {
            title: 'Midbrain',
            text: 'The smallest region of the brainstem, playing a crucial role in vision, hearing, motor control, sleep/wake cycles, alertness, and temperature regulation. It acts as a vital relay center.',
            img: '/images/midbrain-illustration.jpg', // Replace with your image
            backgroundImg: '/images/midbrain-bg.jpg' // Optional background image for the section
        },
        {
            title: 'Pons',
            text: 'Relays information from the cerebrum to the cerebellum. It contains nuclei that deal primarily with sleep, respiration, swallowing, bladder control, hearing, equilibrium, taste, eye movement, facial expressions, facial sensation, and posture.',
            img: '/images/pons-illustration.jpg', // Replace with your image
            backgroundImg: '/images/pons-bg.jpg' // Optional background image for the section
        },
        {
            title: 'Medulla Oblongata',
            text: 'The lowest part of the brainstem, it contains the cardiac, respiratory, vomiting, and vasomotor centers and deals with autonomic (involuntary) functions such as breathing, heart rate, and blood pressure.',
            img: '/images/medulla-illustration.jpg', // Replace with your image
            backgroundImg: '/images/medulla-bg.jpg' // Optional background image for the section
        }
    ];
</script>

<div class="snap-y snap-mandatory h-screen overflow-y-scroll scroll-smooth bg-black font-sans">
    {#each cardData as card, i}
        <div
            class="snap-center flex items-center justify-center px-4 py-8 relative overflow-hidden"
            data-index={i}
            style="min-height: 100vh; background-image: url({card.backgroundImg || 'none'}); background-size: cover; background-position: center; background-attachment: fixed;"
            >
            <div class="absolute inset-0 bg-black/70 z-0"></div>

            <div
                in:fly={{ x: -60, opacity: 0, duration: 800, easing: quintOut }}
                out:fly={{ x: 60, opacity: 0, duration: 500 }}
                class="group flex w-full max-w-5xl flex-col sm:flex-row overflow-hidden rounded-3xl
                       border border-blue-400/20 bg-[rgba(28,28,30,0.8)] shadow-2xl backdrop-blur-lg
                       transition-all duration-500 transform-gpu
                       hover:translate-y-[-10px] hover:scale-[1.02]
                       hover:shadow-[0_25px_70px_rgba(32,201,151,0.3)] hover:border-blue-300/60
                       relative z-10"
            >
                <div class="sm:w-1/2 flex items-center justify-center p-4">
                    <img
                        src={card.img}
                        alt={card.title}
                        class="h-full max-h-80 w-full object-contain rounded-xl shadow-lg
                               transform transition-transform duration-500 group-hover:scale-105"
                    />
                </div>

                <div class="p-8 sm:w-1/2 flex flex-col justify-center text-white">
                    <h2
                        class="text-5xl font-extrabold text-blue-400 mb-4 tracking-tight leading-tight
                                drop-shadow-[0_0_15px_rgba(32,201,151,0.5)]"
                    >
                        {card.title}
                    </h2>
                    <p class="mt-4 text-xl text-gray-200 leading-relaxed">
                        {card.text}
                    </p>
                </div>

                <div
                    class="absolute bottom-0 left-0 w-full h-[6px] bg-gradient-to-r from-blue-400 via-blue-500 to-purple-600
                           transform scale-x-0 origin-left transition-transform duration-700 ease-out group-hover:scale-x-100"
                ></div>
            </div>
        </div>
    {/each}
</div>

<style>
    /* Custom scrollbar for a cleaner look */
    .overflow-y-scroll::-webkit-scrollbar {
        width: 8px;
    }

    .overflow-y-scroll::-webkit-scrollbar-track {
        background: #1a1a1a;
    }

    .overflow-y-scroll::-webkit-scrollbar-thumb {
        background-color: #4a90e2;
        border-radius: 20px;
        border: 2px solid #1a1a1a;
    }

    .overflow-y-scroll::-webkit-scrollbar-thumb:hover {
        background-color: #3f7bbf;
    }
</style>