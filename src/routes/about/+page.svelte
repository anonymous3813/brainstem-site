<script lang="ts">
    import { fade } from 'svelte/transition';
    import { quintOut } from 'svelte/easing';
</script>

<svelte:head>
    <title>About The Brainstem</title>
    <meta name="description" content="Learn more about The Brainstem - our mission, vision, and the technology behind our interactive 3D web experiences built with Svelte and Spline." />
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet" />
</svelte:head>

<div class="bg-gray-950 text-gray-100 py-16">
    <div class="container mx-auto px-4 max-w-6xl">
        <section class="text-center mb-20" in:fade={{ duration: 1000, easing: quintOut }}>
            <h1 class="text-6xl sm:text-7xl lg:text-8xl font-extrabold mb-6 leading-tight
                       text-transparent bg-clip-text bg-gradient-to-r from-teal-400 to-blue-500
                       shadow-teal-glow animate-pulse-light">
                About The Brainstem
            </h1>
            <p class="text-xl md:text-2xl max-w-3xl mx-auto text-gray-300">
                Unveiling the core of interactive web experiences and digital innovation.
            </p>
        </section>

        <section
            class="bg-gray-900 rounded-3xl p-8 md:p-12 shadow-2xl mb-16
                   transform hover:scale-[1.01] transition-transform duration-300 ease-out
                   border border-gray-700"
            in:fade={{ delay: 200, duration: 800 }}
        >
            <h2 class="text-4xl font-bold text-teal-400 mb-6 flex items-center">
                <span class="mr-3 text-5xl">🎯</span> Our Mission
            </h2>
            <p class="text-lg md:text-xl leading-relaxed text-gray-200">
                At The Brainstem, our mission is to redefine digital interaction. We aim to fuse cutting-edge 3D visualization with rich, contextual information, creating web environments that are not just viewed, but experienced. We believe in building bridges between complex data and intuitive understanding, fostering engagement and discovery.
            </p>
        </section>

        <section
            class="bg-gray-900 rounded-3xl p-8 md:p-12 shadow-2xl mb-16
                   transform hover:scale-[1.01] transition-transform duration-300 ease-out
                   border border-gray-700"
            in:fade={{ delay: 400, duration: 800 }}
        >
            <h2 class="text-4xl font-bold text-teal-400 mb-8 flex items-center">
                <span class="mr-3 text-5xl">💡</span> Our Approach
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-10 text-gray-200">
                <div>
                    <h3 class="text-2xl font-semibold text-blue-400 mb-3">Interactive Storytelling</h3>
                    <p class="leading-relaxed text-lg">
                        We leverage the power of Svelte and Spline to craft narratives where users actively participate. Our 3D models aren't static; they respond, guide, and evolve, providing a dynamic backdrop for every piece of information.
                    </p>
                </div>
                <div>
                    <h3 class="text-2xl font-semibold text-blue-400 mb-3">Seamless Integration</h3>
                    <p class="leading-relaxed text-lg">
                        Information and visuals flow together effortlessly. The design principles prioritize clarity and aesthetic harmony, ensuring that every element contributes to a cohesive and memorable journey.
                    </p>
                </div>
                <div>
                    <h3 class="text-2xl font-semibold text-blue-400 mb-3">User-Centric Design</h3>
                    <p class="leading-relaxed text-lg">
                        Every project begins and ends with the user in mind. We strive for interfaces that are intuitive, accessible, and deeply engaging, making complex concepts easy to explore and understand.
                    </p>
                </div>
                <div>
                    <h3 class="text-2xl font-semibold text-blue-400 mb-3">Future-Forward Technologies</h3>
                    <p class="leading-relaxed text-lg">
                        Embracing modern web technologies like Svelte allows us to build highly performant and reactive applications, pushing the boundaries of what's possible in a browser.
                    </p>
                </div>
            </div>
        </section>

        <section
            class="bg-gray-900 rounded-3xl p-8 md:p-12 shadow-2xl
                   transform hover:scale-[1.01] transition-transform duration-300 ease-out
                   border border-gray-700"
            in:fade={{ delay: 600, duration: 800 }}
        >
            <h2 class="text-4xl font-bold text-teal-400 mb-6 flex items-center">
                <span class="mr-3 text-5xl">✨</span> Our Vision
            </h2>
            <p class="text-lg md:text-xl leading-relaxed text-gray-200">
                Our vision is a web where passive consumption is replaced by active exploration. We envision a future where digital content is not just informative, but inherently immersive and captivating, sparking curiosity and facilitating deeper learning for everyone.
            </p>
        </section>
    </div>
</div>

<style>
    /* Custom styles for the hero title's glow and subtle pulse effect */
    .shadow-teal-glow {
        text-shadow: 0 0 15px rgba(0, 255, 255, 0.4), 0 0 30px rgba(0, 255, 255, 0.2);
    }

    /* Subtle pulse animation for the hero title */
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