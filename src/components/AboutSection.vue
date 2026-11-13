<template>
  <section
    id="about"
    :class="[
      'pt-28 pb-20 sm:pt-32 sm:pb-24 transition-colors duration-300',
      isDark ? 'bg-[#0a0a0a] text-white' : 'bg-white text-neutral-900'
    ]"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Top Metadata & Controls Bar (FR/EN & Light/Dark) -->
      <div
        :class="[
          'flex flex-col sm:flex-row sm:items-center justify-between gap-4 pb-5 mb-12 border-b',
          isDark ? 'border-white/10' : 'border-neutral-200'
        ]"
      >
        <p :class="['font-inter text-sm', isDark ? 'text-neutral-400' : 'text-neutral-600']">
          {{ $t('hero.role_bar') }}
        </p>

        <!-- Segmented Controls: Language & Theme -->
        <div class="flex flex-wrap items-center gap-3">
          <!-- Language Switcher -->
          <div
            :class="[
              'inline-flex items-center rounded-lg border p-1 text-xs font-medium',
              isDark ? 'border-white/15 bg-neutral-950' : 'border-neutral-300 bg-neutral-100'
            ]"
            role="group"
            aria-label="Language switcher"
          >
            <button
              type="button"
              @click="locale = 'fr'"
              :class="[
                'inline-flex items-center gap-1.5 px-2.5 py-1 rounded-md transition-colors duration-150 cursor-pointer',
                locale === 'fr'
                  ? (isDark ? 'bg-neutral-800 text-white font-semibold' : 'bg-neutral-900 text-white font-semibold')
                  : (isDark ? 'text-neutral-400 hover:text-white' : 'text-neutral-600 hover:text-neutral-900')
              ]"
            >
              <!-- French Flag SVG -->
              <svg class="w-4 h-3 rounded-[2px] shrink-0" viewBox="0 0 36 24" aria-hidden="true">
                <rect width="12" height="24" fill="#002395" />
                <rect x="12" width="12" height="24" fill="#FFFFFF" />
                <rect x="24" width="12" height="24" fill="#ED2939" />
              </svg>
              <span>FR</span>
            </button>
            <button
              type="button"
              @click="locale = 'en'"
              :class="[
                'inline-flex items-center gap-1.5 px-2.5 py-1 rounded-md transition-colors duration-150 cursor-pointer',
                locale === 'en'
                  ? (isDark ? 'bg-neutral-800 text-white font-semibold' : 'bg-neutral-900 text-white font-semibold')
                  : (isDark ? 'text-neutral-400 hover:text-white' : 'text-neutral-600 hover:text-neutral-900')
              ]"
            >
              <!-- UK / English Flag SVG -->
              <svg class="w-4 h-3 rounded-[2px] shrink-0" viewBox="0 0 60 30" aria-hidden="true">
                <clipPath id="uk-clip">
                  <rect width="60" height="30" />
                </clipPath>
                <g clip-path="url(#uk-clip)">
                  <rect width="60" height="30" fill="#012169" />
                  <path d="M0,0 L60,30 M60,0 L0,30" stroke="#FFFFFF" stroke-width="6" />
                  <path d="M0,0 L60,30 M60,0 L0,30" stroke="#C8102E" stroke-width="3" />
                  <path d="M30,0 v30 M0,15 h60" stroke="#FFFFFF" stroke-width="10" />
                  <path d="M30,0 v30 M0,15 h60" stroke="#C8102E" stroke-width="6" />
                </g>
              </svg>
              <span>EN</span>
            </button>
          </div>

          <!-- Theme Switcher -->
          <div
            :class="[
              'inline-flex items-center rounded-lg border p-1 text-xs font-medium',
              isDark ? 'border-white/15 bg-neutral-950' : 'border-neutral-300 bg-neutral-100'
            ]"
            role="group"
            aria-label="Theme switcher"
          >
            <button
              type="button"
              @click="$emit('set-dark', false)"
              :class="[
                'inline-flex items-center gap-1.5 px-3 py-1 rounded-md transition-colors duration-150 cursor-pointer',
                !isDark
                  ? 'bg-neutral-900 text-white font-semibold'
                  : 'text-neutral-400 hover:text-white'
              ]"
            >
              <!-- Sun SVG Icon -->
              <svg class="w-3.5 h-3.5 shrink-0" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                <circle cx="12" cy="12" r="4" />
                <path d="M12 2v2M12 20v2M4.93 4.93l1.41 1.41M17.66 17.66l1.41 1.41M2 12h2M20 12h2M6.34 17.66l-1.41 1.41M19.07 4.93l-1.41 1.41" />
              </svg>
              <span>Light</span>
            </button>
            <button
              type="button"
              @click="$emit('set-dark', true)"
              :class="[
                'inline-flex items-center gap-1.5 px-3 py-1 rounded-md transition-colors duration-150 cursor-pointer',
                isDark
                  ? 'bg-neutral-800 text-white font-semibold'
                  : 'text-neutral-600 hover:text-neutral-900'
              ]"
            >
              <!-- Moon SVG Icon -->
              <svg class="w-3.5 h-3.5 shrink-0" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z" />
              </svg>
              <span>Dark</span>
            </button>
          </div>
        </div>
      </div>

      <!-- Left-aligned Section Header -->
      <div class="mb-12">
        <div class="flex items-center gap-3 mb-2">
          <span class="w-8 h-0.5 bg-[#E11D48]"></span>
          <span class="text-[#E11D48] font-inter font-semibold text-xs uppercase tracking-widest">
            {{ $t('about.subtitle') }}
          </span>
        </div>
        <h1
          :class="[
            'font-outfit text-3xl sm:text-4xl lg:text-5xl font-bold tracking-tight',
            isDark ? 'text-white' : 'text-neutral-900'
          ]"
        >
          {{ $t('about.title') }}
        </h1>
      </div>

      <!-- Content Grid: Info on Left, Larger Photo on Right -->
      <div class="grid lg:grid-cols-12 gap-12 lg:gap-16 items-center">
        <!-- Left Column: Description, Personal Info, Hobbies, CV -->
        <div class="lg:col-span-6 space-y-8 order-2 lg:order-1">
          <p
            :class="[
              'font-inter text-base sm:text-lg leading-relaxed',
              isDark ? 'text-neutral-300' : 'text-neutral-700'
            ]"
            style="text-wrap: pretty;"
          >
            {{ $t('about.description') }}
          </p>

          <!-- Personal Info Grid -->
          <div class="grid sm:grid-cols-2 gap-4">
            <div
              v-for="item in infoItems"
              :key="item.key"
              :class="[
                'flex items-start gap-3.5 p-4 rounded-xl border transition-colors duration-200',
                isDark
                  ? 'bg-neutral-950 border-white/10 hover:border-[#E11D48]/60'
                  : 'bg-neutral-50 border-neutral-200 hover:border-[#E11D48]/60'
              ]"
            >
              <span class="w-2 h-2 rounded-full bg-[#E11D48] mt-2 flex-shrink-0"></span>
              <div>
                <div
                  :class="[
                    'text-xs font-inter font-semibold uppercase tracking-wider',
                    isDark ? 'text-neutral-400' : 'text-neutral-500'
                  ]"
                >
                  {{ $t(`about.${item.key}`) }}
                </div>
                <div
                  :class="[
                    'text-sm font-inter font-medium mt-0.5',
                    isDark ? 'text-white' : 'text-neutral-900'
                  ]"
                >
                  {{ item.value }}
                </div>
              </div>
            </div>
          </div>

          <!-- Hobbies -->
          <div>
            <div
              :class="[
                'text-xs font-inter font-semibold uppercase tracking-wider mb-3',
                isDark ? 'text-neutral-400' : 'text-neutral-500'
              ]"
            >
              {{ $t('about.hobbies') }}
            </div>
            <div class="flex flex-wrap gap-2.5">
              <span
                v-for="hobby in hobbies"
                :key="hobby"
                :class="[
                  'px-3.5 py-1.5 rounded-lg text-sm font-inter font-medium border',
                  isDark
                    ? 'bg-neutral-950 border-white/10 text-neutral-200'
                    : 'bg-neutral-50 border-neutral-200 text-neutral-800'
                ]"
              >
                {{ hobby }}
              </span>
            </div>
          </div>

          <!-- Action Buttons -->
          <div class="flex flex-wrap items-center gap-4 pt-2">
            <a
              href="#contact"
              @click.prevent="$emit('scroll-to', 'contact')"
              class="inline-flex items-center gap-2.5 px-6 py-3.5 bg-[#E11D48] hover:bg-[#BE123C] text-white font-inter text-sm font-semibold rounded-lg transition-colors duration-200"
            >
              <span>⬇</span>
              <span>{{ $t('about.download_cv') }}</span>
            </a>

            <button
              type="button"
              @click="$emit('scroll-to', 'projects')"
              :class="[
                'inline-flex items-center justify-center gap-2.5 px-6 py-3.5 rounded-lg border font-inter text-sm font-semibold transition-colors duration-200 cursor-pointer',
                isDark
                  ? 'border-white/20 text-white hover:border-white/40 hover:bg-white/5'
                  : 'border-neutral-300 text-neutral-900 hover:border-neutral-900 hover:bg-neutral-50'
              ]"
            >
              <span>{{ $t('hero.cta_primary') }}</span>
              <span aria-hidden="true">↘</span>
            </button>
          </div>
        </div>

        <!-- Right Column: Larger Portrait without badges -->
        <div class="lg:col-span-6 order-1 lg:order-2 flex justify-center lg:justify-end">
          <div
            :class="[
              'relative w-full max-w-lg lg:max-w-xl aspect-[4/4.6] rounded-2xl overflow-hidden border',
              isDark ? 'border-white/15 bg-neutral-900' : 'border-neutral-200 bg-neutral-100'
            ]"
          >
            <img
              src="/profil.JPG"
              alt="Hapsatou Thiam"
              class="w-full h-full object-cover object-top"
              fetchpriority="high"
            />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'

defineProps({ isDark: Boolean })
defineEmits(['scroll-to', 'set-dark'])

const { locale } = useI18n()

const infoItems = computed(() => [
  { key: 'phone', value: '+221 78-150-96-80' },
  { key: 'email', value: 'thiamhapsatou@gmail.com' },
  { key: 'location', value: locale.value === 'fr' ? 'Thiès, Sénégal' : 'Thiès, Senegal' },
  { key: 'languages', value: 'Français, English, Pullar, Wolof' },
])

const hobbies = computed(() => [
  locale.value === 'fr' ? 'Lecture' : 'Reading',
  locale.value === 'fr' ? 'Voyage' : 'Travel',
  locale.value === 'fr' ? 'Cuisine' : 'Cooking',
])
</script>
