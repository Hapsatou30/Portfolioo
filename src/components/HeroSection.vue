<template>
  <section
    id="home"
    :class="[
      'min-h-dvh pt-24 pb-16 sm:pt-28 sm:pb-24 transition-colors duration-300',
      isDark ? 'bg-[#0a0a0a] text-white' : 'bg-white text-neutral-900'
    ]"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Top Metadata & Controls Bar -->
      <div
        :class="[
          'flex flex-col sm:flex-row sm:items-center justify-between gap-4 pb-5 mb-12 lg:mb-16 border-b',
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
            <span :class="['px-2 select-none', isDark ? 'text-neutral-400' : 'text-neutral-500']" aria-hidden="true">
              🌐
            </span>
            <button
              type="button"
              @click="locale = 'fr'"
              :class="[
                'px-2.5 py-1 rounded-md transition-colors duration-150 cursor-pointer',
                locale === 'fr'
                  ? (isDark ? 'bg-neutral-800 text-white font-semibold' : 'bg-neutral-900 text-white font-semibold')
                  : (isDark ? 'text-neutral-400 hover:text-white' : 'text-neutral-600 hover:text-neutral-900')
              ]"
            >
              FR
            </button>
            <button
              type="button"
              @click="locale = 'en'"
              :class="[
                'px-2.5 py-1 rounded-md transition-colors duration-150 cursor-pointer',
                locale === 'en'
                  ? (isDark ? 'bg-neutral-800 text-white font-semibold' : 'bg-neutral-900 text-white font-semibold')
                  : (isDark ? 'text-neutral-400 hover:text-white' : 'text-neutral-600 hover:text-neutral-900')
              ]"
            >
              EN
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
              <span aria-hidden="true">☀</span>
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
              <span aria-hidden="true">☾</span>
              <span>Dark</span>
            </button>
          </div>
        </div>
      </div>

      <!-- Main Hero Grid -->
      <div class="grid lg:grid-cols-12 gap-10 lg:gap-14 items-center">
        <!-- Left Column: Copy & CTAs -->
        <div class="lg:col-span-6 flex flex-col justify-between space-y-8">
          <div class="space-y-6">
            <h1
              :class="[
                'font-outfit font-bold tracking-tight leading-[1.08] text-4xl sm:text-5xl lg:text-[3.4rem]',
                isDark ? 'text-white' : 'text-neutral-900'
              ]"
              style="text-wrap: balance;"
            >
              {{ $t('hero.headline') }}
            </h1>

            <p
              :class="[
                'font-inter text-base sm:text-lg leading-relaxed max-w-xl',
                isDark ? 'text-neutral-400' : 'text-neutral-600'
              ]"
              style="text-wrap: pretty;"
            >
              {{ $t('hero.subtitle') }}
            </p>
          </div>

          <!-- Action Buttons -->
          <div class="flex flex-wrap items-center gap-4 pt-2">
            <button
              type="button"
              @click="$emit('scroll-to', 'projects')"
              class="inline-flex items-center justify-center gap-2.5 px-6 py-3.5 rounded-lg bg-[#E11D48] hover:bg-[#BE123C] text-white font-inter text-sm font-semibold transition-colors duration-200 cursor-pointer"
            >
              <span>{{ $t('hero.cta_primary') }}</span>
              <span aria-hidden="true">↘</span>
            </button>

            <a
              href="#contact"
              @click.prevent="$emit('scroll-to', 'contact')"
              :class="[
                'inline-flex items-center justify-center gap-2.5 px-6 py-3.5 rounded-lg border font-inter text-sm font-semibold transition-colors duration-200',
                isDark
                  ? 'border-white/20 text-white hover:border-white/40 hover:bg-white/5'
                  : 'border-neutral-300 text-neutral-900 hover:border-neutral-900 hover:bg-neutral-50'
              ]"
            >
              <span aria-hidden="true">📄</span>
              <span>{{ $t('hero.cta_secondary') }}</span>
            </a>
          </div>
        </div>

        <!-- Right Column: Larger Portrait Card -->
        <div class="lg:col-span-6 flex justify-center lg:justify-end">
          <div
            :class="[
              'relative w-full max-w-lg lg:max-w-xl rounded-2xl overflow-hidden border aspect-[4/4.6]',
              isDark ? 'border-white/10 bg-neutral-900' : 'border-neutral-200 bg-neutral-100'
            ]"
          >
            <img
              src="/profil.JPG"
              alt="Hapsatou Thiam"
              class="w-full h-full object-cover object-top"
              fetchpriority="high"
            />

            <!-- Clean solid bottom caption bar -->
            <div class="absolute inset-x-0 bottom-0 bg-neutral-950/85 px-6 py-4 border-t border-white/10">
              <p class="font-outfit text-sm font-semibold text-white">
                {{ $t('hero.caption_title') }}
              </p>
              <p class="font-inter text-xs text-neutral-300 mt-0.5">
                {{ $t('hero.caption_sub') }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { useI18n } from 'vue-i18n'

defineProps({
  isDark: Boolean,
})

defineEmits(['scroll-to', 'set-dark'])

const { locale } = useI18n()
</script>
