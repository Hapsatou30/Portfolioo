<template>
  <section
    id="experience"
    :class="[
      'py-24 border-t transition-colors duration-300',
      isDark ? 'bg-[#0a0a0a] border-white/10 text-white' : 'bg-white border-neutral-200 text-neutral-900'
    ]"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Left-aligned Section Header -->
      <div class="mb-16">
        <div class="flex items-center gap-3 mb-2">
          <span class="w-8 h-0.5 bg-[#E11D48]"></span>
          <span class="text-[#E11D48] font-inter font-semibold text-xs uppercase tracking-widest">
            {{ $t('experience.subtitle') }}
          </span>
        </div>
        <h2
          :class="[
            'font-outfit text-3xl sm:text-4xl lg:text-5xl font-bold tracking-tight',
            isDark ? 'text-white' : 'text-neutral-900'
          ]"
        >
          {{ $t('experience.title') }}
        </h2>
      </div>

      <div class="grid lg:grid-cols-12 gap-12 lg:gap-14 items-start">
        <!-- Work Experience Column (Left 6 Cols) -->
        <div class="lg:col-span-6 space-y-6">
          <div class="flex items-center justify-between border-b pb-4" :class="isDark ? 'border-white/10' : 'border-neutral-200'">
            <div class="flex items-center gap-3">
              <span class="w-9 h-9 rounded-full bg-[#E11D48] text-white font-outfit font-bold text-sm flex items-center justify-center">
                01
              </span>
              <h3 :class="['font-outfit text-2xl font-bold tracking-tight', isDark ? 'text-white' : 'text-neutral-900']">
                {{ $t('experience.work') }}
              </h3>
            </div>
            <span class="px-3 py-1 rounded-full bg-[#E11D48]/15 text-[#E11D48] font-inter text-xs font-bold uppercase tracking-wider">
              PRO
            </span>
          </div>

          <!-- Featured Work Card -->
          <div
            :class="[
              'group relative rounded-2xl border p-7 sm:p-8 transition-all duration-300 hover:-translate-y-1',
              isDark
                ? 'bg-neutral-950 border-white/15 hover:border-[#E11D48]'
                : 'bg-neutral-50 border-neutral-200 hover:border-[#E11D48] hover:bg-white'
            ]"
          >
            <!-- Solid Red Accent Bar on Left -->
            <div class="absolute top-6 bottom-6 left-0 w-1 bg-[#E11D48] rounded-r-full"></div>

            <!-- Header Badge + Company -->
            <div class="flex flex-wrap items-center justify-between gap-3 mb-6">
              <span class="inline-flex items-center gap-2 px-3.5 py-1.5 rounded-full bg-[#E11D48] text-white text-xs font-inter font-semibold">
                <span class="w-1.5 h-1.5 rounded-full bg-white animate-pulse"></span>
                {{ $t('experience.web_dev_period') }}
              </span>

              <span
                :class="[
                  'font-mono text-xs font-semibold px-3 py-1 rounded-md border',
                  isDark ? 'border-white/10 bg-white/5 text-neutral-300' : 'border-neutral-200 bg-white text-neutral-700'
                ]"
              >
                Thiès / Sénégal
              </span>
            </div>

            <h4 :class="['font-outfit font-bold text-2xl sm:text-3xl tracking-tight', isDark ? 'text-white' : 'text-neutral-900']">
              {{ $t('experience.web_dev_title') }}
            </h4>
            <p class="font-inter text-base font-semibold text-[#E11D48] mt-1 mb-6">
              {{ $t('experience.web_dev_company') }}
            </p>

            <!-- Structured Tasks List -->
            <div class="space-y-3.5">
              <div
                v-for="(task, i) in workTasks"
                :key="i"
                :class="[
                  'flex items-start gap-3.5 p-3.5 rounded-xl border transition-colors duration-200',
                  isDark
                    ? 'bg-black/60 border-white/10 group-hover:border-white/20'
                    : 'bg-white border-neutral-200/80'
                ]"
              >
                <span class="w-6 h-6 rounded-full bg-[#E11D48] text-white font-mono text-xs font-bold flex items-center justify-center shrink-0 mt-0.5">
                  {{ i + 1 }}
                </span>
                <p :class="['text-sm font-inter leading-relaxed', isDark ? 'text-neutral-300' : 'text-neutral-700']">
                  {{ task }}
                </p>
              </div>
            </div>
          </div>
        </div>

        <!-- Education Column (Right 6 Cols) -->
        <div class="lg:col-span-6 space-y-6">
          <div class="flex items-center justify-between border-b pb-4" :class="isDark ? 'border-white/10' : 'border-neutral-200'">
            <div class="flex items-center gap-3">
              <span
                :class="[
                  'w-9 h-9 rounded-full font-outfit font-bold text-sm flex items-center justify-center border-2 border-[#E11D48]',
                  isDark ? 'bg-neutral-950 text-white' : 'bg-white text-neutral-900'
                ]"
              >
                02
              </span>
              <h3 :class="['font-outfit text-2xl font-bold tracking-tight', isDark ? 'text-white' : 'text-neutral-900']">
                {{ $t('experience.education') }}
              </h3>
            </div>
            <span
              :class="[
                'px-3 py-1 rounded-full font-inter text-xs font-bold uppercase tracking-wider border',
                isDark ? 'border-white/15 text-neutral-300' : 'border-neutral-300 text-neutral-700'
              ]"
            >
              ACADÉMIQUE
            </span>
          </div>

          <!-- Interactive Connected Education Timeline -->
          <div class="relative pl-6 sm:pl-8 space-y-5 before:content-[''] before:absolute before:top-4 before:bottom-4 before:left-[11px] sm:before:left-[15px] before:w-0.5 before:bg-[#E11D48]">
            <div
              v-for="(edu, idx) in educationItems"
              :key="edu.titleKey"
              class="relative group"
            >
              <!-- Circular Stepper Node -->
              <span
                :class="[
                  'absolute -left-6 sm:-left-8 top-6 w-6 h-6 sm:w-8 sm:h-8 rounded-full border-2 border-[#E11D48] flex items-center justify-center font-mono text-xs font-bold transition-colors duration-200 z-10',
                  idx === 0
                    ? 'bg-[#E11D48] text-white'
                    : (isDark
                        ? 'bg-[#0a0a0a] text-white group-hover:bg-[#E11D48]'
                        : 'bg-white text-neutral-900 group-hover:bg-[#E11D48] group-hover:text-white')
                ]"
              >
                0{{ idx + 1 }}
              </span>

              <!-- Education Card -->
              <div
                :class="[
                  'p-6 rounded-2xl border transition-all duration-200 group-hover:-translate-y-1',
                  isDark
                    ? 'bg-neutral-950 border-white/15 group-hover:border-[#E11D48]'
                    : 'bg-neutral-50 border-neutral-200 group-hover:border-[#E11D48] group-hover:bg-white'
                ]"
              >
                <div class="flex items-center justify-between flex-wrap gap-2 mb-2">
                  <span class="px-3 py-1 rounded-full bg-[#E11D48] text-white font-mono text-xs font-bold">
                    {{ $t(`experience.${edu.periodKey}`) }}
                  </span>
                  <span :class="['font-mono text-xs uppercase tracking-wider', isDark ? 'text-neutral-500' : 'text-neutral-500']">
                    {{ edu.badge }}
                  </span>
                </div>

                <h4 :class="['font-outfit font-bold text-lg sm:text-xl mt-2', isDark ? 'text-white' : 'text-neutral-900']">
                  {{ $t(`experience.${edu.titleKey}`) }}
                </h4>

                <div class="flex items-center gap-2 mt-2">
                  <span class="w-2 h-2 rounded-full bg-[#E11D48]"></span>
                  <span :class="['font-inter text-sm font-medium', isDark ? 'text-neutral-300' : 'text-neutral-700']">
                    {{ $t(`experience.${edu.schoolKey}`) }}
                  </span>
                </div>
              </div>
            </div>
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
const { tm } = useI18n()

const workTasks = computed(() => tm('experience.web_dev_tasks'))

const educationItems = [
  {
    titleKey: 'edu_cert_title',
    schoolKey: 'edu_cert_school',
    periodKey: 'edu_cert_period',
    badge: 'Certification',
  },
  {
    titleKey: 'edu_bachelor_title',
    schoolKey: 'edu_bachelor_school',
    periodKey: 'edu_bachelor_period',
    badge: 'Licence / Bachelor',
  },
  {
    titleKey: 'edu_bac_title',
    schoolKey: 'edu_bac_school',
    periodKey: 'edu_bac_period',
    badge: 'Diplôme d’État',
  },
]
</script>
