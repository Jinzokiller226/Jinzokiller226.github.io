<script setup lang="ts">
import { ref } from 'vue'
import { RouterLink, RouterView, useRoute } from 'vue-router'
import { watch } from 'vue'

const open = ref(false)
const route = useRoute()

// close the mobile menu after navigating
watch(() => route.fullPath, () => (open.value = false))

const links = [
  { to: '/', label: 'Home', icon: 'm4 12 8-8 8 8M6 10.5V19a1 1 0 0 0 1 1h3v-3a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1v3h3a1 1 0 0 0 1-1v-8.5' },
  { to: '/about', label: 'Experience', icon: 'M12 6.03v13m0-13c-2.819-.831-4.715-1.076-8.029-1.023A.99.99 0 0 0 3 6v11c0 .563.466 1.014 1.03 1.007 3.122-.043 5.018.212 7.97 1.023m0-13c2.819-.831 4.715-1.076 8.029-1.023A.99.99 0 0 1 21 6v11c0 .563-.466 1.014-1.03 1.007-3.122-.043-5.018.212-7.97 1.023' },
  { to: '/techstack', label: 'Techstack', icon: 'M7.99999 10.8571 12 13.1428m-4.00001-2.2857L4 13.1428m3.99999-2.2857.00004-4.57139M12 13.1428v4.5715m0-4.5715-4.00001 2.2857M12 13.1428l4-2.2857m-4 2.2857V8.57143m0 4.57137 4 2.2858m-4 2.2857L7.99999 20M12 17.7143 16 20m-8.00001 0L4 17.7143v-4.5715M7.99999 20v-4.5715M4 13.1428l3.99999 2.2857M16 6.28571 12 4 8.00003 6.28571m7.99997 0v4.57139m0-4.57139-4 2.28572m4 2.28567 4 2.2858M8.00003 6.28571 12 8.57143m8 4.57147v4.5714L16 20m4-6.8571-4 2.2857M16 20v-4.5714' },
  { to: '/projects', label: 'Projects', icon: 'M10 3v4a1 1 0 0 1-1 1H5m14-4v16a1 1 0 0 1-1 1H6a1 1 0 0 1-1-1V7.914a1 1 0 0 1 .293-.707l3.914-3.914A1 1 0 0 1 9.914 3H18a1 1 0 0 1 1 1Z' },
  { to: '/contactme', label: 'Contact', icon: 'M18.427 14.768 17.2 13.542a1.733 1.733 0 0 0-2.45 0l-.613.613a1.732 1.732 0 0 1-2.45 0l-1.838-1.84a1.735 1.735 0 0 1 0-2.452l.612-.613a1.735 1.735 0 0 0 0-2.452L9.237 5.572a1.6 1.6 0 0 0-2.45 0c-3.223 3.2-1.702 6.896 1.519 10.117 3.22 3.221 6.914 4.745 10.12 1.535a1.601 1.601 0 0 0 0-2.456Z' },
]
</script>

<template>
  <div
    class="min-h-screen w-screen overflow-x-hidden overflow-y-auto bg-gray-900/50 bg-[url('../assets/bg.jpg')] bg-cover bg-fixed bg-center bg-no-repeat"
  >
    <div class="mx-auto flex min-h-screen w-full max-w-screen-xl flex-col px-4 sm:px-6">
      <!-- Navbar -->
      <nav class="sticky top-0 z-50 py-3">
        <div
          class="rounded-2xl bg-transparent px-4 py-2 shadow-[0_8px_32px_0_rgba(0,0,0,0.2)] backdrop-blur-[11px]"
        >
          <!-- Mobile: hamburger button -->
          <div class="flex items-center justify-end md:hidden">
            <button
              type="button"
              class="inline-flex h-11 w-11 items-center justify-center rounded-lg text-white hover:bg-white/10 focus:outline-none focus-visible:ring-2 focus-visible:ring-white/60"
              :aria-expanded="open"
              aria-controls="navbar-user"
              aria-label="Toggle navigation menu"
              @click="open = !open"
            >
              <svg v-if="!open" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2" stroke-linecap="round">
                <path d="M4 6h16M4 12h16M4 18h16" />
              </svg>
              <svg v-else class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2" stroke-linecap="round">
                <path d="M6 6l12 12M18 6L6 18" />
              </svg>
            </button>
          </div>

          <!-- Links: hidden on phones until toggled, always visible from md up -->
          <div id="navbar-user" :class="[open ? 'block' : 'hidden', 'md:block']">
            <ul
              class="mt-2 flex flex-col gap-1 font-medium md:mt-0 md:flex-row md:items-center md:justify-end md:gap-10"
            >
              <li v-for="l in links" :key="l.to">
                <RouterLink
                  :to="l.to"
                  class="flex items-center gap-2 rounded-lg px-3 py-3 text-white hover:bg-white/10 md:px-0 md:py-1 md:hover:bg-transparent md:hover:text-blue-300"
                  active-class="bg-white/10 md:bg-transparent md:text-blue-300"
                >
                  <svg class="h-6 w-6 shrink-0" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="l.icon" />
                  </svg>
                  {{ l.label }}
                </RouterLink>
              </li>
            </ul>
          </div>
        </div>
      </nav>

      <!-- Page content -->
      <main class="flex-1 shadow-[0_8px_32px_0_rgba(0,0,0,0.2)] backdrop-blur-[11px]">
        <RouterView v-slot="{ Component }">
          <transition
            appear
            enter-active-class="transition-all duration-500 ease-in"
            enter-from-class="opacity-0 translate-y-4"
            enter-to-class="opacity-100 translate-y-0"
            leave-active-class="transition-all duration-300 ease-out"
            leave-from-class="opacity-100"
            leave-to-class="opacity-0"
            mode="out-in"
          >
            <component :is="Component" />
          </transition>
        </RouterView>
      </main>
    </div>
  </div>
</template>