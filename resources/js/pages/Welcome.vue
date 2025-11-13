<script setup lang="ts">
import { dashboard, login, register } from '@/routes';
import { Head, Link } from '@inertiajs/vue3';
import { ref, computed, onMounted, onUnmounted } from 'vue';
import AboutJerkshead from '@/components/AboutJerkshead.vue';

withDefaults(
    defineProps<{
        canRegister: boolean;
    }>(),
    {
        canRegister: true,
    },
);

// Parallax scroll state
const scrollY = ref(0);
const clamp = (val: number, min: number, max: number) => Math.min(Math.max(val, min), max);
const handleScroll = () => {
    scrollY.value = window.scrollY || document.documentElement.scrollTop || 0;
};
onMounted(() => {
    handleScroll();
    window.addEventListener('scroll', handleScroll, { passive: true });
});
onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll);
});

const easeOutQuad = (t: number) => 1 - (1 - t) * (1 - t);
const progressRaw = computed(() => clamp(scrollY.value / 400, 0, 1));
const progress = computed(() => easeOutQuad(progressRaw.value));

// Title parallax: slight lift and scale as you scroll
const titleStyle = computed(() => {
    const y = -progress.value * 20; // move up to 20px (slower)
    const scale = 1 + progress.value * 0.02; // scale up to 2% (subtle)
    return {
        transform: `translateY(${y}px) scale(${scale})`,
        willChange: 'transform',
    } as const;
});

// Right paragraph parallax: ease the tilt and push forward while lifting
const paragraphStyle = computed(() => {
    const rotateY = -35 + progress.value * 6; // -35deg -> -29deg
    const translateZ = 30 + progress.value * 15; // 30px -> 45px
    const translateY = -progress.value * 12; // lift up to 12px
    return {
        transform: `perspective(900px) rotateY(${rotateY}deg) skewX(-6deg) translateZ(${translateZ}px) translateY(${translateY}px)`,
        willChange: 'transform',
    } as const;
});
</script>

<template>
    <Head title="Welcome">
        <link rel="preconnect" href="https://rsms.me/" />
        <link rel="stylesheet" href="https://rsms.me/inter/inter.css" />
        <link rel="stylesheet" href="https://fonts.cdnfonts.com/css/dharma-gothic-m" />
    </Head>

    <main class="relative h-screen">
        <img
            src="/storage/images/findjerks.png"
            alt="FindJerks Landing Image"
            class="h-full w-full object-cover"
        />

        <!-- Title graphic centered at the bottom -->
        <div
            class="absolute bottom-8 left-1/2 -translate-x-1/2 transition-transform duration-700 ease-out will-change-transform"
            :style="titleStyle"
        >
            <img
                src="/storage/images/title.png"
                alt="FindJerks Title"
                class="h-auto w-[70vw] max-w-[400px] drop-shadow-[0_4px_20px_rgba(0,0,0,0.6)]"
            />
        </div>

        <!-- 3D-style right-side paragraph, slightly skewed left -->
        <div class="absolute right-6 top-1/2 -translate-y-1/2 max-w-md hidden md:block">
            <div
                class="relative select-none text-white transition-transform duration-700 ease-out will-change-transform"
                :style="paragraphStyle"
            >
                <p class="text-5xl md:text-6xl font-extrabold uppercase tracking-wide leading-tight text-[#f2dc2f] [text-shadow:0_1px_0_#c3a91f,0_2px_0_#b1971c,0_3px_0_#9e8619,0_4px_0_#8c7616,0_5px_0_#7a6614,0_6px_0_#6a5712,0_14px_28px_rgba(0,0,0,.65)]">
                    The jerks won’t hide forever.
                </p>
                <p class="mt-3 text-white/90 text-lg font-medium">
                    Scan the area, trust your gut, and pin the location fast.
                </p>
            </div>
        </div>
    </main>



    <!-- About Jerkshead: left image, right text with specific fonts -->
    <AboutJerkshead />

</template>
