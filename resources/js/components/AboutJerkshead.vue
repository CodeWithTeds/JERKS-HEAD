<template>
    <!-- About Jerkshead: left image, right text with specific fonts -->
    <section id="about-jerkshead" class="bg-[#4B4A44] text-white px-6 py-20">
        <div class="mx-auto max-w-6xl grid grid-cols-1 md:grid-cols-2 gap-10 items-center">
            <!-- Left: Image -->
            <div class="relative order-1 md:order-none">
                <img
                    src="/storage/images/image.png"
                    alt="Jerkshead reference visual"
                    class="w-full aspect-[4/3] rounded-xl border border-neutral-800 shadow-xl object-cover"
                    loading="lazy"
                />
            </div>

            <!-- Right: Text -->
            <!-- 3D-style right-side paragraph, slightly skewed left -->
            <div class="order-2 md:order-none">
                <h2
                    class="font-normal text-[40px] leading-[70px] tracking-tight uppercase text-[#f2dc2f] [text-shadow:0_1px_0_#c3a91f,0_2px_0_#b1971c,0_3px_0_#9e8619,0_4px_0_#8c7616,0_5px_0_#7a6614,0_6px_0_#6a5712,0_14px_28px_rgba(0,0,0,.65)]"
                    style="font-family: 'dharma-gothic-m', sans-serif"
                >
                    FIND JERKSHEAD
                </h2>
                <p
                    class="mt-4 text-[20px] leading-[23px] font-normal text-white/85"
                    style="font-family: 'Times', 'Times New Roman', serif"
                >
                    Somewhere in the Philippines, Jerkshead is hiding. Maybe in the bustling streets of Quiapo,
                    or perhaps on the sun-drenched beaches of Siargao. Your mission? To find him before anyone else does.
                </p>
                <p
                    class="mt-3 text-[20px] leading-[23px] font-normal text-white/85"
                    style="font-family: 'Times', 'Times New Roman', serif"
                >
                    Jerkshead is a web-based multiplayer game where observation, speed, and local knowledge are your best tools.
                    Each round challenges you to locate Jerkshead’s hiding spot — the closer you get, the more points you earn.
                    Compete against friends or players from across the country, and prove who knows the 7,641 islands best.
                </p>
            </div>
        </div>
    </section>
</template>