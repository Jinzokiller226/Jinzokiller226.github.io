<script setup lang="ts">
import avatar from '../assets/avatar3nobg.png' // swap for any avatar image, or use the #avatar slot

interface TechItem {
  name: string
  mark: string // short letter mark shown in the badge
  color: string // hex badge color
  note: string
}

// Typed slot: lets parents pass <template #avatar> with editor support.
defineSlots<{
  avatar?(): unknown
}>()

const backend: TechItem[] = [
  { name: 'Laravel', mark: 'L', color: '#FF2D20', note: 'Routing, Eloquent models, auth and queues for internal systems.' },
  { name: 'PHP', mark: 'php', color: '#777BB4', note: 'The language behind the back end and its automation scripts.' },
  { name: 'Livewire', mark: 'Lw', color: '#FB70A9', note: 'Reactive components without leaving Blade.' },
]

const frontend: TechItem[] = [
  { name: 'Vue.js', mark: 'V', color: '#42B883', note: 'Interactive interfaces and single-page views.' },
  { name: 'Tailwind CSS', mark: 'Tw', color: '#38BDF8', note: 'Utility-first styling for responsive layouts.' },
  { name: 'Flowbite', mark: 'Fb', color: '#1C64F2', note: 'Ready-made components on top of Tailwind.' },
]
</script>

<template>
  <section class="mx-auto w-full max-w-7xl px-6 py-12 md:py-12">
    <header class="mb-10 max-w-2xl text-left md:mb-14">
      <h2 class="text-3xl font-semibold tracking-tight text-white md:text-4xl">Tech stack</h2>
      <p class="mt-3 text-slate-300">
        The tools I use every day to build and support web applications, from the database to the browser.
      </p>
    </header>

    <div class="grid items-center gap-10 md:grid-cols-[1fr_minmax(16rem,22rem)_1fr] md:gap-8">
      <!-- Back end -->
      <div class="order-2 md:order-1">
        <h3 class="mb-4 text-sm font-medium text-slate-400 md:text-right">Back end</h3>
        <ul class="space-y-5">
          <li
            v-for="t in backend"
            :key="t.name"
            class="flex items-start gap-4 md:flex-row-reverse md:text-right"
          >
            <span
              class="grid h-11 w-11 shrink-0 place-items-center rounded-xl text-sm font-bold text-white"
              :style="{ backgroundColor: t.color }"
              aria-hidden="true"
            >
              {{ t.mark }}
            </span>
            <div>
              <p class="font-semibold text-white">{{ t.name }}</p>
              <p class="mt-0.5 text-sm text-slate-300">{{ t.note }}</p>
            </div>
          </li>
        </ul>
      </div>

      <!-- Avatar space -->
      <div class="relative order-1 mx-auto w-full max-w-xs md:order-2 md:max-w-none">
        <div
          class="pointer-events-none absolute inset-x-4 bottom-4 top-8 rounded-full bg-blue-600/25 blur-3xl"
          aria-hidden="true"
        />
        <div
          class="pointer-events-none absolute bottom-0 left-1/2 h-5 w-3/4 -translate-x-1/2 rounded-[50%] bg-black/50 blur-xl"
          aria-hidden="true"
        />

        <div class="relative z-10 flex aspect-[4/5] items-end justify-center">
          <slot name="avatar">
            <img
              v-if="avatar"
              :src="avatar"
              alt="3D avatar of me with a laptop"
              class="h-full w-full object-contain drop-shadow-[0_20px_30px_rgba(0,0,0,0.45)]"
              draggable="false"
            />
            <div
              v-else
              class="grid h-full w-full place-items-center rounded-3xl border-2 border-dashed border-slate-600 text-sm text-slate-400"
            >
              Avatar goes here
            </div>
          </slot>
        </div>
      </div>

      <!-- Front end -->
      <div class="order-3">
        <h3 class="mb-4 text-sm font-medium text-slate-400">Front end</h3>
        <ul class="space-y-5">
          <li v-for="t in frontend" :key="t.name" class="flex items-start gap-4">
            <span
              class="grid h-11 w-11 shrink-0 place-items-center rounded-xl text-sm font-bold text-white"
              :style="{ backgroundColor: t.color }"
              aria-hidden="true"
            >
              {{ t.mark }}
            </span>
            <div>
              <p class="font-semibold text-white">{{ t.name }}</p>
              <p class="mt-0.5 text-sm text-slate-300">{{ t.note }}</p>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>