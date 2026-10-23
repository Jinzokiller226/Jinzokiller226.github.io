<script setup lang="ts">
import { ref } from 'vue'
import avatar from '../assets/avatar4nobg.png' // copy avatar4.png into src/assets

interface Duty {
  title: string
  text: string
}

interface Tilt {
  x: number
  y: number
}

const duties: Duty[] = [
  {
    title: 'Application Support',
    text: 'Write new functions for the current automated system, fix front-end and back-end bugs, and support the end users and operations teams who rely on it.',
  },
  {
    title: 'Web Development',
    text: 'Build and maintain web features for internal tools, from the interface down to the database queries behind it.',
  },
]

// Pointer tilt: the avatar turns slightly toward the cursor.
const stage = ref<HTMLDivElement | null>(null)
const tilt = ref<Tilt>({ x: 0, y: 0 })
const reduceMotion =
  typeof window !== 'undefined' &&
  window.matchMedia('(prefers-reduced-motion: reduce)').matches

function onMove(e: PointerEvent): void {
  if (reduceMotion || !stage.value) return
  const r = stage.value.getBoundingClientRect()
  const px = (e.clientX - r.left) / r.width - 0.5
  const py = (e.clientY - r.top) / r.height - 0.5
  tilt.value = { x: py * -8, y: px * 10 }
}
function onLeave(): void {
  tilt.value = { x: 0, y: 0 }
}
</script>

<template>
  <section
    class="mx-auto grid w-full max-w-7xl items-center gap-10 px-6 py-12 md:grid-cols-[1.1fr_0.9fr] md:py-20"
  >
    <!-- Text -->
    <div class="order-2 text-left md:order-1">
      <h1 class="text-3xl font-semibold tracking-tight text-white md:text-4xl">
        MIS Specialist: Application Support / Junior Web Developer
      </h1>

      <Transition
        appear
        enter-active-class="transition-all duration-700 ease-out"
        enter-from-class="opacity-0 translate-y-3"
        enter-to-class="opacity-100 translate-y-0"
      >
        <h2 class="mt-3 text-lg text-slate-300 md:text-xl">
          Vanguard Screening Solutions Inc. (Pasig City, Philippines)
        </h2>
      </Transition>

      <ul class="mt-8 space-y-6 border-l-2 border-blue-500/60 pl-5">
        <li v-for="d in duties" :key="d.title">
          <h3 class="text-lg font-semibold text-white">{{ d.title }}</h3>
          <p class="mt-1 max-w-prose text-slate-300">{{ d.text }}</p>
        </li>
      </ul>
    </div>

    <!-- Avatar -->
    <div
      ref="stage"
      class="relative order-1 mx-auto flex w-full max-w-sm items-end justify-center md:order-2 md:max-w-md"
      style="perspective: 1000px"
      @pointermove="onMove"
      @pointerleave="onLeave"
    >
      <!-- blue glow, echoes the server LEDs -->
      <div
        class="pointer-events-none absolute inset-x-6 bottom-6 top-10 rounded-full bg-blue-600/25 blur-3xl"
        aria-hidden="true"
      />
      <!-- floor shadow -->
      <div
        class="pointer-events-none absolute bottom-1 h-6 w-3/4 rounded-[50%] bg-black/50 blur-xl"
        aria-hidden="true"
      />

      <img
        :src="avatar"
        alt="3D avatar of me holding a laptop beside a server rack"
        class="relative z-10 h-auto max-h-[560px] w-full object-contain drop-shadow-[0_20px_30px_rgba(0,0,0,0.45)] transition-transform duration-200 ease-out will-change-transform"
        :style="{
          transform: `rotateX(${tilt.x}deg) rotateY(${tilt.y}deg)`,
        }"
        draggable="false"
      />
    </div>
  </section>
</template>