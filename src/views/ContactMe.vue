<script setup lang="ts">
import { reactive, ref } from 'vue'
import avatar from '../assets/avatar4nobg.png' // swap for any avatar image, or use the #avatar slot

interface ContactForm {
  name: string
  email: string
  message: string
}

type FormErrors = Partial<Record<keyof ContactForm, string>>
type Status = 'idle' | 'sending' | 'sent' | 'error'

interface ContactLink {
  label: string
  value: string
  href: string
}

interface Props {
  /** Where the default mailto fallback sends messages. */
  email?: string
  /** Optional async handler, e.g. a call to your Laravel API. Throw to show an error. */
  submitHandler?: (data: ContactForm) => Promise<void>
  links?: ContactLink[]
}

const props = withDefaults(defineProps<Props>(), {
  email: 'your.email@example.com', // TODO: replace with your real email
  submitHandler: undefined,
  links: () => [
    { label: 'Location', value: 'Quezon City, Philippines', href: '' }
  ],
})

const emit = defineEmits<{
  (e: 'submit', payload: ContactForm): void
}>()

defineSlots<{
  avatar?(): unknown
}>()

const form = reactive<ContactForm>({ name: '', email: '', message: '' })
const errors = ref<FormErrors>({})
const status = ref<Status>('idle')

const EMAIL_PATTERN = /^[^\s@]+@[^\s@]+\.[^\s@]+$/

function validate(): boolean {
  const next: FormErrors = {}
  if (!form.name.trim()) next.name = 'Enter your name.'
  if (!EMAIL_PATTERN.test(form.email.trim())) next.email = 'Enter a valid email address.'
  if (form.message.trim().length < 10) next.message = 'Write at least 10 characters.'
  errors.value = next
  return Object.keys(next).length === 0
}

function resetForm(): void {
  form.name = ''
  form.email = ''
  form.message = ''
}

async function onSubmit(): Promise<void> {
  if (!validate()) return

  const payload: ContactForm = {
    name: form.name.trim(),
    email: form.email.trim(),
    message: form.message.trim(),
  }
  emit('submit', payload)
  status.value = 'sending'

  try {
    if (props.submitHandler) {
      await props.submitHandler(payload)
    } else {
      // Fallback with no backend: open the visitor's email app.
      const subject = encodeURIComponent(`Portfolio message from ${payload.name}`)
      const body = encodeURIComponent(`${payload.message}\n\nFrom: ${payload.name} (${payload.email})`)
      window.location.href = `mailto:${props.email}?subject=${subject}&body=${body}`
    }
    status.value = 'sent'
    resetForm()
  } catch {
    status.value = 'error'
  }
}

const inputClass =
  'block w-full rounded-lg border border-white/10 bg-slate-900/60 px-4 py-4 text-white placeholder-slate-500 transition focus:border-blue-500 focus:outline-none focus:ring-2 focus:ring-blue-500/40'
</script>

<template>
  <section class="mx-auto w-full max-w-6xl px-6 py-12 md:py-12">
   <h2 class="text-2xl font-semibold tracking-tight text-white md:text-4xl">Contact me</h2>

    <div class="grid items-center gap-10 md:grid-cols-[0.8fr_1.2fr] md:gap-14">
      <!-- Avatar and contact details -->
      <div class="mx-auto w-full max-w-xs md:max-w-sm">
        <div class="relative">
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
                alt="3D avatar of me waving from beside a server rack"
                class="h-sm w-full object-contain drop-shadow-[0_20px_30px_rgba(0,0,0,0.45)]"
                draggable="false"
              />
            </slot>
          </div>
        </div>

        <ul class="mt-8 space-y-3">
          <li v-for="l in links" :key="l.label" class="text-left">
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

      <!-- Form -->
      <form
        class="rounded-2xl border border-white/10 bg-white/5 p-6 backdrop-blur-sm md:p-8"
        novalidate
        @submit.prevent="onSubmit"
      >
        <div class="grid gap-5 sm:grid-cols-2">
            
          <div>
            
            <label for="contact-name" class="mb-4 block text-sm font-medium text-slate-300">Name</label>
            <input
              id="contact-name"
              v-model="form.name"
              type="text"
              autocomplete="name"
              placeholder="Juan Dela Cruz"
              :class="inputClass"
              :aria-invalid="!!errors.name"
              aria-describedby="contact-name-error"
            />
            <p v-if="errors.name" id="contact-name-error" class="mt-1 text-sm text-red-400">
              {{ errors.name }}
            </p>
          </div>

          <div>
            <label for="contact-email" class="mb-2 block text-sm font-medium text-slate-300">Email</label>
            <input
              id="contact-email"
              v-model="form.email"
              type="email"
              autocomplete="email"
              placeholder="name@company.com"
              :class="inputClass"
              :aria-invalid="!!errors.email"
              aria-describedby="contact-email-error"
            />
            <p v-if="errors.email" id="contact-email-error" class="mt-1 text-sm text-red-400">
              {{ errors.email }}
            </p>
          </div>
        </div>

        <div class="mt-5">
          <label for="contact-message" class="mb-2 block text-sm font-medium text-slate-300">Message</label>
          <textarea
            id="contact-message"
            v-model="form.message"
            rows="6"
            placeholder="Tell me about your project or role."
            :class="inputClass"
            :aria-invalid="!!errors.message"
            aria-describedby="contact-message-error"
          />
          <p v-if="errors.message" id="contact-message-error" class="mt-1 text-sm text-red-400">
            {{ errors.message }}
          </p>
        </div>

        <div class="mt-6 flex flex-wrap items-center gap-4">
          <button
            type="submit"
            :disabled="status === 'sending'"
            class="rounded-lg bg-blue-600 px-6 py-3 text-sm font-medium text-white transition hover:bg-blue-500 focus:outline-none focus-visible:ring-2 focus-visible:ring-blue-300 disabled:cursor-not-allowed disabled:opacity-60"
          >
            {{ status === 'sending' ? 'Sending…' : 'Send message' }}
          </button>

          <p v-if="status === 'sent'" class="text-sm text-emerald-400" role="status">
            Message ready. Thank you for reaching out.
          </p>
          <p v-else-if="status === 'error'" class="text-sm text-red-400" role="alert">
            Your message could not be sent. Try again, or email me directly at {{ email }}.
          </p>
        </div>
      </form>
    </div>
  </section>
</template>