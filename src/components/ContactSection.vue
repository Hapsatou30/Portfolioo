<template>
  <section
    id="contact"
    :class="[
      'py-24 border-t transition-colors duration-300',
      isDark ? 'bg-[#0a0a0a] border-white/10 text-white' : 'bg-white border-neutral-200 text-neutral-900'
    ]"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Left-aligned Section Header -->
      <div class="mb-14">
        <div class="flex items-center gap-3 mb-2">
          <span class="w-8 h-0.5 bg-[#E11D48]"></span>
          <span class="text-[#E11D48] font-inter font-semibold text-xs uppercase tracking-widest">
            {{ $t('contact.subtitle') }}
          </span>
        </div>
        <h2
          :class="[
            'font-outfit text-3xl sm:text-4xl lg:text-5xl font-bold tracking-tight',
            isDark ? 'text-white' : 'text-neutral-900'
          ]"
        >
          {{ $t('contact.title') }}
        </h2>
      </div>

      <div class="grid lg:grid-cols-12 gap-12 lg:gap-16">
        <!-- Contact Info -->
        <div class="lg:col-span-5 space-y-6">
          <p :class="['font-inter text-base sm:text-lg leading-relaxed', isDark ? 'text-neutral-300' : 'text-neutral-700']">
            {{ locale === 'fr'
              ? "Vous avez un projet ou une opportunité ? N'hésitez pas à me contacter ! Je suis ouverte à de nouvelles collaborations et défis."
              : "Have a project or opportunity? Feel free to reach out! I'm open to new collaborations and challenges."
            }}
          </p>

          <div class="space-y-4">
            <a
              v-for="info in contactInfo"
              :key="info.labelKey"
              :href="info.href"
              :class="[
                'flex items-center gap-4 p-4 rounded-xl border transition-colors duration-200',
                isDark
                  ? 'bg-neutral-950 border-white/10 hover:border-[#E11D48]'
                  : 'bg-neutral-50 border-neutral-200 hover:border-[#E11D48]'
              ]"
            >
              <div class="w-11 h-11 rounded-lg bg-[#E11D48] text-white flex items-center justify-center text-base font-bold flex-shrink-0">
                {{ info.symbol }}
              </div>
              <div>
                <div :class="['text-xs font-inter font-semibold uppercase tracking-wider', isDark ? 'text-neutral-400' : 'text-neutral-500']">
                  {{ $t(`contact.${info.labelKey}`) }}
                </div>
                <div :class="['font-inter text-sm font-medium mt-0.5', isDark ? 'text-white' : 'text-neutral-900']">
                  {{ info.value }}
                </div>
              </div>
            </a>
          </div>
        </div>

        <!-- Contact Form -->
        <div
          :class="[
            'lg:col-span-7 p-6 sm:p-8 rounded-2xl border',
            isDark ? 'bg-neutral-950 border-white/10' : 'bg-neutral-50 border-neutral-200'
          ]"
        >
          <form @submit.prevent="submitForm" class="space-y-5">
            <div>
              <label :class="['block text-sm font-inter font-medium mb-2', isDark ? 'text-neutral-300' : 'text-neutral-700']">
                {{ $t('contact.name_label') }}
              </label>
              <input
                v-model="form.name"
                type="text"
                name="name"
                required
                :placeholder="locale === 'fr' ? 'Votre nom complet' : 'Your full name'"
                :class="[
                  'w-full px-4 py-3 rounded-lg font-inter text-sm transition-colors duration-200 outline-none border',
                  isDark
                    ? 'bg-black border-white/15 text-white placeholder-neutral-500 focus:border-[#E11D48]'
                    : 'bg-white border-neutral-300 text-neutral-900 placeholder-neutral-400 focus:border-[#E11D48]'
                ]"
              />
            </div>

            <div>
              <label :class="['block text-sm font-inter font-medium mb-2', isDark ? 'text-neutral-300' : 'text-neutral-700']">
                {{ $t('contact.email_label') }}
              </label>
              <input
                v-model="form.email"
                type="email"
                name="email"
                required
                :placeholder="locale === 'fr' ? 'votre@email.com' : 'your@email.com'"
                :class="[
                  'w-full px-4 py-3 rounded-lg font-inter text-sm transition-colors duration-200 outline-none border',
                  isDark
                    ? 'bg-black border-white/15 text-white placeholder-neutral-500 focus:border-[#E11D48]'
                    : 'bg-white border-neutral-300 text-neutral-900 placeholder-neutral-400 focus:border-[#E11D48]'
                ]"
              />
            </div>

            <div>
              <label :class="['block text-sm font-inter font-medium mb-2', isDark ? 'text-neutral-300' : 'text-neutral-700']">
                {{ $t('contact.message_label') }}
              </label>
              <textarea
                v-model="form.message"
                name="message"
                required
                rows="5"
                :placeholder="locale === 'fr' ? 'Décrivez votre projet...' : 'Tell me about your project...'"
                :class="[
                  'w-full px-4 py-3 rounded-lg font-inter text-sm transition-colors duration-200 outline-none border resize-y',
                  isDark
                    ? 'bg-black border-white/15 text-white placeholder-neutral-500 focus:border-[#E11D48]'
                    : 'bg-white border-neutral-300 text-neutral-900 placeholder-neutral-400 focus:border-[#E11D48]'
                ]"
              ></textarea>
            </div>

            <p v-if="errorMsg" class="text-xs font-inter font-medium text-[#E11D48]">
              {{ errorMsg }}
            </p>

            <button
              type="submit"
              :disabled="loading || sent"
              class="w-full py-3.5 bg-[#E11D48] hover:bg-[#BE123C] text-white font-inter text-sm font-semibold rounded-lg transition-colors duration-200 cursor-pointer disabled:opacity-60 disabled:cursor-not-allowed"
            >
              <span v-if="loading">{{ locale === 'fr' ? 'Envoi en cours...' : 'Sending...' }}</span>
              <span v-else-if="sent">{{ $t('contact.success') }}</span>
              <span v-else>{{ $t('contact.send') }}</span>
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import { useI18n } from 'vue-i18n'

defineProps({ isDark: Boolean })
const { locale } = useI18n()

// Linked Google Spreadsheet: https://docs.google.com/spreadsheets/d/1t0zl3Yxa_-2WJoiwVjy68ThHvO2zwgaEJYGeDC49HRQ/edit?gid=0#gid=0
const GOOGLE_SHEET_ID = '1t0zl3Yxa_-2WJoiwVjy68ThHvO2zwgaEJYGeDC49HRQ'
const GOOGLE_DEPLOYMENT_ID = 'AKfycbzp1sGMcHgsmAlCj_RSaXVdNpejdRd7Ccd6lZrfMH0xwudZH07DMhU02QkZ9oaj50Uv1g'
const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbzp1sGMcHgsmAlCj_RSaXVdNpejdRd7Ccd6lZrfMH0xwudZH07DMhU02QkZ9oaj50Uv1g/exec'

const form = ref({ name: '', email: '', message: '' })
const loading = ref(false)
const sent = ref(false)
const errorMsg = ref('')

async function submitForm() {
  loading.value = true
  errorMsg.value = ''

  const payload = {
    spreadsheetId: GOOGLE_SHEET_ID,
    deploymentId: GOOGLE_DEPLOYMENT_ID,
    date: new Date().toISOString(),
    name: form.value.name,
    email: form.value.email,
    message: form.value.message,
  }

  try {
    if (GOOGLE_SCRIPT_URL) {
      const formData = new FormData()
      Object.entries(payload).forEach(([key, value]) => formData.append(key, value))

      await fetch(GOOGLE_SCRIPT_URL, {
        method: 'POST',
        mode: 'no-cors',
        body: formData,
      })
    }

    sent.value = true
    form.value = { name: '', email: '', message: '' }
    setTimeout(() => {
      sent.value = false
    }, 4000)
  } catch (err) {
    errorMsg.value = locale.value === 'fr'
      ? "Une erreur s'est produite lors de l'envoi. Veuillez réessayer."
      : 'An error occurred while sending. Please try again.'
  } finally {
    loading.value = false
  }
}

const contactInfo = [
  { labelKey: 'phone', symbol: '☎', value: '+221 78-150-96-80', href: 'tel:+221781509680' },
  { labelKey: 'email', symbol: '✉', value: 'thiamhapsatou@gmail.com', href: 'mailto:thiamhapsatou@gmail.com' },
  { labelKey: 'location', symbol: '⌖', value: 'Thiès, Sénégal', href: '#contact' },
]
</script>
