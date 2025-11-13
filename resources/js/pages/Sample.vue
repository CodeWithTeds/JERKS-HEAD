<script setup lang="ts">
import { Head } from '@inertiajs/vue3';
import { ref, computed, onMounted, onUnmounted } from 'vue';

// Scroll tracking for parallax
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

const progress = computed(() => clamp(scrollY.value / 600, 0, 1));

// Title parallax: lift and scale subtly
const titleStyle = computed(() => {
  const y = -progress.value * 30;
  const scale = 1 + progress.value * 0.03;
  return {
    transform: `translateX(-50%) translateY(${y}px) scale(${scale})`,
    willChange: 'transform',
  } as const;
});

// Right paragraph parallax: ease tilt, push forward, lift
const paragraphStyle = computed(() => {
  const rotateY = -35 + progress.value * 8;
  const translateZ = 30 + progress.value * 20;
  const translateY = -progress.value * 18;
  return {
    transform: `perspective(900px) rotateY(${rotateY}deg) skewX(-6deg) translateZ(${translateZ}px) translateY(${translateY}px)`,
    willChange: 'transform',
  } as const;
});
</script>

<template>
  <Head title="Sample Parallax" />

  <!-- Scrollable page with fixed hero background -->
  <main class="relative min-h-[220vh] overflow-x-hidden bg-black">
    <img
      src="/storage/images/findjerks.png"
      alt="Background"
      class="fixed inset-0 h-screen w-screen object-cover"
    />

    <!-- Title graphic bottom center with parallax -->
    <div class="fixed bottom-8 left-1/2 will-change-transform" :style="titleStyle">
      <img
        src="/storage/images/title.png"
        alt="FindJerks Title"
        class="h-auto w-[70vw] max-w-[420px] drop-shadow-[0_4px_20px_rgba(0,0,0,0.6)]"
      />
    </div>

    <!-- 3D-style right-side paragraph (hidden on phones) -->
    <div class="fixed right-6 top-1/2 -translate-y-1/2 max-w-md hidden md:block">
      <div class="relative select-none text-white transition-transform duration-300 ease-out will-change-transform" :style="paragraphStyle">
        <p class="text-5xl md:text-6xl font-extrabold uppercase tracking-wide leading-tight text-[#f2dc2f] [text-shadow:0_1px_0_#c3a91f,0_2px_0_#b1971c,0_3px_0_#9e8619,0_4px_0_#8c7616,0_5px_0_#7a6614,0_6px_0_#6a5712,0_14px_28px_rgba(0,0,0,.65)]">
          The jerks won’t hide forever.
        </p>
        <p class="mt-3 text-white/90 text-lg font-medium">
          Scan the area, trust your gut, and pin the location fast.
        </p>
      </div>
    </div>

    <!-- Scroll filler content to demonstrate parallax -->
    <section class="relative z-10 pt-[105vh] px-6 md:px-10 text-white space-y-12">
      <div class="max-w-3xl">
        <h2 class="text-2xl md:text-3xl font-semibold">Sample Parallax Page</h2>
        <p class="mt-2 text-white/80">
          Scroll to see the title lift and the right paragraph ease forward with a subtle 3D tilt. This page is intentionally tall so you can feel the motion.
        </p>
      </div>

      <div class="grid md:grid-cols-2 gap-8 max-w-6xl">
        <div class="bg-white/5 rounded-lg p-6 ring-1 ring-white/10">
          <h3 class="text-xl font-medium">What’s going on?</h3>
          <p class="mt-2 text-white/80">We track scroll progress and apply transform changes for a lightweight parallax illusion. No heavy libraries required.</p>
        </div>
        <div class="bg-white/5 rounded-lg p-6 ring-1 ring-white/10">
          <h3 class="text-xl font-medium">Try different speeds</h3>
          <p class="mt-2 text-white/80">Adjust progress scaling to make the motion stronger or gentler depending on your taste.</p>
        </div>
      </div>

      <div class="h-[60vh]" />
    </section>
  </main>
</template>