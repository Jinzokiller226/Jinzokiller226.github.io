<script setup lang="ts">
interface Language {
  name: string
  color: string // hex, e.g. '#4F5D95'
}

interface Project {
  name: string
  kind: string
  description: string
  languages: Language[]
  tools: string[]
  repo: string
  commits: number
}

// Edit this array to add, remove or reword projects.
// Language colors follow GitHub's language colors.
const projects: Project[] = [
  {
    name: 'app_insystem',
    kind: 'Web application',
    description:
      'A project directory system built on Laravel. Includes the standard Laravel structure for routes, database migrations, Blade views and PHPUnit tests, with Vite and Tailwind CSS for the front end.',
    languages: [
      { name: 'PHP', color: '#4F5D95' },
      { name: 'Blade', color: '#F7523F' },
      { name: 'JavaScript', color: '#F1E05A' },
      { name: 'CSS', color: '#663399' },
    ],
    tools: ['Laravel', 'Tailwind CSS', 'Vite', 'Composer'],
    repo: 'https://github.com/Jinzokiller226/app_insystem',
    commits: 22,
  },
  {
    name: 'Sample-Mobile-App',
    kind: 'Mobile application',
    description:
      'A sample mobile app written in Kotlin and built with Gradle. Started from the Google AI Studio repository template.',
    languages: [{ name: 'Kotlin', color: '#A97BFF' }],
    tools: ['Gradle (Kotlin DSL)'],
    repo: 'https://github.com/Jinzokiller226/Sample-Mobile-App',
    commits: 3,
  },
]
</script>

<template>
  <section class="mx-auto w-full max-w-7xl px-4 py-10 sm:px-6 md:py-14 lg:px-8 lg:py-16">
    <header class="mb-8 max-w-2xl text-left sm:mb-10 md:mb-14">
      <h2 class="text-2xl font-semibold tracking-tight text-white sm:text-3xl md:text-4xl">
        Projects
      </h2>
      <p class="mt-3 text-sm text-slate-300 sm:text-base">
        Public repositories from my GitHub, with the languages each one is written in.
      </p>
    </header>

    <!-- 1 column on phones, as many columns as fit (min ~22rem) on larger screens -->
    <div class="grid grid-cols-1 gap-4 sm:gap-6 lg:grid-cols-2">
      <article
        v-for="p in projects"
        :key="p.name"
        class="flex min-w-0 flex-col rounded-2xl border border-white/10 bg-white/5 p-4 backdrop-blur-sm sm:p-6"
      >
        <p class="text-xs text-blue-400 sm:text-sm">{{ p.kind }}</p>
        <h3 class="mt-1 break-words font-mono text-lg font-semibold text-white sm:text-xl">
          {{ p.name }}
        </h3>

        <p class="mt-3 text-sm leading-relaxed text-slate-300 sm:mt-4 sm:text-base">
          {{ p.description }}
        </p>

        <!-- Languages -->
        <div class="mt-5 sm:mt-6">
          <p class="mb-2 text-xs font-medium text-slate-400 sm:text-sm">Languages</p>
          <ul class="flex flex-wrap gap-2">
            <li
              v-for="l in p.languages"
              :key="l.name"
              class="inline-flex items-center gap-2 rounded-full border border-white/10 bg-white/5 px-3 py-1 text-xs text-white sm:text-sm"
            >
              <span
                class="h-2.5 w-2.5 shrink-0 rounded-full"
                :style="{ backgroundColor: l.color }"
                aria-hidden="true"
              />
              {{ l.name }}
            </li>
          </ul>
        </div>

        <!-- Frameworks and tools -->
        <div class="mt-4 sm:mt-5">
          <p class="mb-2 text-xs font-medium text-slate-400 sm:text-sm">Built with</p>
          <ul class="flex flex-wrap gap-2">
            <li
              v-for="t in p.tools"
              :key="t"
              class="rounded-md bg-slate-800 px-2.5 py-1 text-xs text-slate-200 sm:text-sm"
            >
              {{ t }}
            </li>
          </ul>
        </div>

        <!-- Footer: stacked on phones, side-by-side from sm up. mt-auto pins it to the card bottom -->
        <div
          class="mt-auto flex flex-col gap-3 pt-6 sm:flex-row sm:items-center sm:justify-between sm:gap-4 sm:pt-8"
        >
          <span class="text-xs text-slate-400 sm:text-sm">{{ p.commits }} commits</span>
          <a
            :href="p.repo"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex min-h-11 w-full items-center justify-center gap-2 rounded-lg bg-blue-600 px-4 py-2 text-sm font-medium text-white transition hover:bg-blue-500 focus:outline-none focus-visible:ring-2 focus-visible:ring-blue-300 sm:w-auto"
          >
            View on GitHub
            <svg class="h-4 w-4 shrink-0" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
              <path d="M11 3a1 1 0 100 2h2.59L8.3 10.3a1 1 0 101.4 1.4L15 6.41V9a1 1 0 102 0V4a1 1 0 00-1-1h-5z" />
              <path d="M5 5a2 2 0 00-2 2v8a2 2 0 002 2h8a2 2 0 002-2v-3a1 1 0 10-2 0v3H5V7h3a1 1 0 000-2H5z" />
            </svg>
          </a>
        </div>
      </article>
    </div>
  </section>
</template>