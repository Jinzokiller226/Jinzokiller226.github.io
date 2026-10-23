<script setup lang="ts">
import { computed, onBeforeUnmount, ref } from 'vue'
import avatar from '../assets/avatar4nobg.png' // swap for any avatar image, or use the #avatar slot

interface ContactLink {
  label: string
  value: string
  href: string
}

interface Props {
  email?: string
  /** Pre-filled subject line for the visitor's email app. */
  subject?: string
  links?: ContactLink[]
}

const props = withDefaults(defineProps<Props>(), {
  email: 'venas.francisagustin@gmail.com',
  subject: 'Hello from your portfolio',
  links: () => [
    { label: 'GitHub', value: 'Jinzokiller226', href: 'https://github.com/Jinzokiller226' },
    { label: 'Location', value: 'Quezon City, Philippines', href: '' },
  ],
})

defineSlots<{
  avatar?(): unknown
}>()

const copied = ref<boolean>(false)
const copyFailed = ref<boolean>(false)
let resetTimer: ReturnType<typeof setTimeout> | undefined

const mailtoHref = computed<string>(
  () => `mailto:${props.email}?subject=${encodeURIComponent(props.subject)}`,
)

function flash(target: typeof copied | typeof copyFailed): void {
  copied.value = false
  copyFailed.value = false
  target.value = true
  if (resetTimer) clearTimeout(resetTimer)
  resetTimer = setTimeout(() => {
    target.value = false
  }, 2500)
}

async function copyEmail(): Promise<void> {
  try {
    await navigator.clipboard.writeText(props.email)
    flash(copied)
  } catch {
    flash(copyFailed)
  }
}

onBeforeUnmount(() => {
  if (resetTimer) clearTimeout(resetTimer)
})
</script>

<template>
  <section class="mx-auto w-full max-w-4xl px-6 py-12 md:py-12">
    <header class="mb-3 max-w-2xl text-left md:mb-14">
      <h2 class="text-3xl font-semibold tracking-tight text-white md:text-4xl">Email me</h2>
      <p class="mt-3 text-slate-300">
        Have a project, a question or a job opening? Send me an email and I will get back to you.
      </p>
    </header>

    <div class="grid items-center gap-10 md:grid-cols-[0.8fr_1.2fr] md:gap-14">
      <!-- Avatar -->
      <div class="relative mx-auto w-full max-w-xs md:max-w-sm">
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
              :src="avatar"
              alt="3D avatar of me beside a server rack"
              class="h-full w-full object-contain drop-shadow-[0_20px_30px_rgba(0,0,0,0.45)]"
              draggable="false"
            />
          </slot>
        </div>
      </div>

      <!-- Email panel -->
      <div class="rounded-2xl border border-white/10 bg-white/5 p-6 text-left backdrop-blur-sm md:p-8">
        <p class="text-sm text-slate-400">Email address</p>
        <a
          :href="mailtoHref"
          class="mt-1 block break-all text-xl font-semibold text-white underline-offset-4 hover:underline focus:outline-none focus-visible:ring-2 focus-visible:ring-blue-400 sm:text-2xl"
        >
          {{ email }}
        </a>

        <div class="mt-6 flex flex-wrap items-center gap-3">
          <a
            :href="mailtoHref"
            class="inline-flex items-center gap-2 rounded-lg bg-blue-600 px-6 py-3 text-sm font-medium text-white transition hover:bg-blue-500 focus:outline-none focus-visible:ring-2 focus-visible:ring-blue-300"
          >
            <svg class="h-4 w-4" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
              <path d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884z" />
              <path d="M18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z" />
            </svg>
            Send an email
          </a>

          <button
            type="button"
            class="rounded-lg border border-white/15 px-6 py-3 text-sm font-medium text-white transition hover:bg-white/10 focus:outline-none focus-visible:ring-2 focus-visible:ring-blue-300"
            @click="copyEmail"
          >
            Copy address
          </button>

          <p v-if="copied" class="text-sm text-emerald-400" role="status">Address copied.</p>
          <p v-else-if="copyFailed" class="text-sm text-red-400" role="alert">
            Copy failed. Select the address above and copy it manually.
          </p>
        </div>

        <ul class="mt-8 grid gap-4 border-t border-white/10 pt-6 sm:grid-cols-2">
          <li v-for="l in links" :key="l.label">
            <p class="text-sm text-slate-400">{{ l.label }}</p>
            <a
              v-if="l.href"
              :href="l.href"
              target="_blank"
              rel="noopener noreferrer"
              class="font-medium text-white underline-offset-4 hover:underline focus:outline-none focus-visible:ring-2 focus-visible:ring-blue-400"
            >
              {{ l.value }}
            </a>
            <p v-else class="font-medium text-white">{{ l.value }}</p>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>