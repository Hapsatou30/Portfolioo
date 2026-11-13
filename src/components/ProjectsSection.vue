<template>
  <section
    id="projects"
    :class="[
      'py-24 border-t transition-colors duration-300',
      isDark ? 'bg-[#0a0a0a] border-white/10 text-white' : 'bg-white border-neutral-200 text-neutral-900'
    ]"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Left-aligned Section Header -->
      <div class="flex flex-col sm:flex-row sm:items-end justify-between gap-4 mb-16">
        <div>
          <div class="flex items-center gap-3 mb-2">
            <span class="w-8 h-0.5 bg-[#E11D48]"></span>
            <span class="text-[#E11D48] font-inter font-semibold text-xs uppercase tracking-widest">
              {{ $t('projects.subtitle') }}
            </span>
          </div>
          <h2
            :class="[
              'font-outfit text-3xl sm:text-4xl lg:text-5xl font-bold tracking-tight',
              isDark ? 'text-white' : 'text-neutral-900'
            ]"
          >
            {{ $t('projects.title') }}
          </h2>
        </div>

        <div
          :class="[
            'inline-flex items-center gap-2 px-4 py-2 rounded-full border font-mono text-xs font-semibold self-start sm:self-auto',
            isDark ? 'border-white/15 bg-neutral-950 text-neutral-300' : 'border-neutral-300 bg-neutral-100 text-neutral-700'
          ]"
        >
          <span class="w-2 h-2 rounded-full bg-[#E11D48]"></span>
          <span>04 {{ $t('projects.title') }}</span>
        </div>
      </div>

      <!-- Lively 2-Column Showcase Grid -->
      <div class="grid md:grid-cols-2 gap-8 lg:gap-10">
        <article
          v-for="(project, index) in projects"
          :key="project.titleKey"
          :class="[
            'group relative flex flex-col justify-between rounded-2xl overflow-hidden border transition-all duration-300 hover:-translate-y-2',
            isDark
              ? 'bg-neutral-950 border-white/15 hover:border-[#E11D48]'
              : 'bg-neutral-50 border-neutral-200 hover:border-[#E11D48] hover:bg-white'
          ]"
        >
          <!-- Top Browser / Screenshot Container -->
          <div>
            <div
              :class="[
                'flex items-center justify-between px-4 py-3 border-b',
                isDark ? 'bg-black border-white/10' : 'bg-neutral-100 border-neutral-200'
              ]"
            >
              <div class="flex items-center gap-2">
                <span class="w-2.5 h-2.5 rounded-full bg-[#E11D48]"></span>
                <span :class="['w-2.5 h-2.5 rounded-full', isDark ? 'bg-white/20' : 'bg-neutral-300']"></span>
                <span :class="['w-2.5 h-2.5 rounded-full', isDark ? 'bg-white/20' : 'bg-neutral-300']"></span>
              </div>
              <span
                :class="[
                  'font-mono text-xs px-3 py-0.5 rounded-full border',
                  isDark ? 'bg-neutral-950 border-white/10 text-neutral-400' : 'bg-white border-neutral-200 text-neutral-600'
                ]"
              >
                {{ project.domain }}
              </span>
              <span class="font-mono text-xs font-bold text-[#E11D48]">
                0{{ index + 1 }}
              </span>
            </div>

            <!-- Project Cover Screenshot -->
            <a
              :href="project.url"
              target="_blank"
              rel="noopener"
              class="block relative aspect-[16/10] overflow-hidden bg-neutral-900"
            >
              <img
                :src="project.image"
                :alt="$t(`projects.${project.titleKey}`)"
                class="w-full h-full object-cover object-top transition-transform duration-500 group-hover:scale-105"
                loading="lazy"
              />

              <!-- Solid Action Pill on Hover -->
              <div class="absolute inset-0 bg-black/55 opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-center justify-center">
                <span class="inline-flex items-center gap-2 px-5 py-2.5 rounded-full bg-[#E11D48] text-white font-inter text-xs sm:text-sm font-semibold transform translate-y-2 group-hover:translate-y-0 transition-transform duration-300">
                  <span>{{ $t('projects.visit') }}</span>
                  <span>↗</span>
                </span>
              </div>
            </a>
          </div>

          <!-- Project Details -->
          <div class="p-6 sm:p-8 flex-1 flex flex-col justify-between space-y-6">
            <div>
              <div class="flex items-center justify-between gap-3 mb-2">
                <span class="text-xs font-inter font-bold uppercase tracking-wider text-[#E11D48]">
                  {{ $t(`projects.${project.categoryKey}`) }}
                </span>
              </div>

              <h3 :class="['font-outfit font-bold text-2xl sm:text-3xl tracking-tight mb-3', isDark ? 'text-white' : 'text-neutral-900']">
                {{ $t(`projects.${project.titleKey}`) }}
              </h3>

              <p :class="['font-inter text-sm sm:text-base leading-relaxed', isDark ? 'text-neutral-400' : 'text-neutral-600']">
                {{ $t(`projects.${project.descKey}`) }}
              </p>
            </div>

            <!-- Bottom Direct Link Bar -->
            <div
              :class="[
                'pt-5 border-t flex items-center justify-between',
                isDark ? 'border-white/10' : 'border-neutral-200'
              ]"
            >
              <a
                :href="project.url"
                target="_blank"
                rel="noopener"
                class="inline-flex items-center gap-2.5 px-5 py-2.5 rounded-lg bg-[#E11D48] hover:bg-[#BE123C] text-white font-inter text-sm font-semibold transition-colors duration-200"
              >
                <span>{{ $t('projects.visit') }}</span>
                <span>↗</span>
              </a>

              <a
                :href="project.url"
                target="_blank"
                rel="noopener"
                :class="[
                  'w-10 h-10 rounded-full border flex items-center justify-center text-sm font-bold transition-colors duration-200',
                  isDark
                    ? 'border-white/15 text-white group-hover:border-[#E11D48] group-hover:bg-[#E11D48]'
                    : 'border-neutral-300 text-neutral-900 group-hover:border-[#E11D48] group-hover:bg-[#E11D48] group-hover:text-white'
                ]"
                :aria-label="$t(`projects.${project.titleKey}`)"
              >
                ↗
              </a>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup>
defineProps({ isDark: Boolean })

const projects = [
  {
    titleKey: 'rahma_title',
    categoryKey: 'rahma_category',
    descKey: 'rahma_desc',
    url: 'https://rahmadelivery.com/',
    domain: 'rahmadelivery.com',
    image: '/projects-rahma.jpg',
  },
  {
    titleKey: 'myschool_title',
    categoryKey: 'myschool_category',
    descKey: 'myschool_desc',
    url: 'https://www.myschool221.com/',
    domain: 'myschool221.com',
    image: '/projects-myschool.jpg',
  },
  {
    titleKey: 'elanpro_title',
    categoryKey: 'elanpro_category',
    descKey: 'elanpro_desc',
    url: 'https://ktechsolutions.cloud/connexion',
    domain: 'ktechsolutions.cloud',
    image: '/projects-elanpro.jpg',
  },
  {
    titleKey: 'iris_title',
    categoryKey: 'iris_category',
    descKey: 'iris_desc',
    url: 'https://iris-sage-mu.vercel.app/',
    domain: 'iris-sage-mu.vercel.app',
    image: '/projects-iris.jpg',
  },
]
</script>
