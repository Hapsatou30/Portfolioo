<template>
  <section
    id="skills"
    :class="[
      'py-24 transition-colors duration-300 overflow-hidden',
      isDark ? 'bg-[#0a0a0a] text-white' : 'bg-white text-neutral-900'
    ]"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Left-aligned Section Header + Category Filter Pills -->
      <div class="flex flex-col lg:flex-row lg:items-end justify-between gap-6 mb-14">
        <div>
          <div class="flex items-center gap-3 mb-2">
            <span class="w-8 h-0.5 bg-[#E11D48]"></span>
            <span class="text-[#E11D48] font-inter font-semibold text-xs uppercase tracking-widest">
              {{ $t('skills.subtitle') }}
            </span>
          </div>
          <h2
            :class="[
              'font-outfit text-3xl sm:text-4xl lg:text-5xl font-bold tracking-tight',
              isDark ? 'text-white' : 'text-neutral-900'
            ]"
          >
            {{ $t('skills.title') }}
          </h2>
        </div>

        <!-- Interactive Category Filter Tabs -->
        <div
          :class="[
            'inline-flex flex-wrap items-center gap-1.5 p-1.5 rounded-xl border self-start lg:self-auto',
            isDark ? 'bg-neutral-950 border-white/10' : 'bg-neutral-100 border-neutral-200'
          ]"
          role="tablist"
        >
          <button
            v-for="tab in filterTabs"
            :key="tab.id"
            type="button"
            role="tab"
            :aria-selected="activeFilter === tab.id"
            @click="activeFilter = tab.id"
            :class="[
              'px-4 py-2 rounded-lg font-inter text-xs sm:text-sm font-semibold transition-all duration-200 cursor-pointer',
              activeFilter === tab.id
                ? 'bg-[#E11D48] text-white'
                : (isDark ? 'text-neutral-400 hover:text-white' : 'text-neutral-600 hover:text-neutral-900')
            ]"
          >
            {{ tab.label }}
          </button>
        </div>
      </div>

      <!-- Main Layout: Interactive Dynamic Orbit Wheel (Left) + Circular Tech Nodes (Right) -->
      <div class="grid lg:grid-cols-12 gap-12 lg:gap-10 items-center">
        <!-- Left: Dynamic Rotating Circular Orbit System -->
        <div class="lg:col-span-6 flex justify-center items-center py-6">
          <div class="relative w-[330px] h-[330px] sm:w-[440px] sm:h-[440px] flex items-center justify-center select-none">
            <!-- Outer Orbit Ring -->
            <div
              :class="[
                'absolute inset-0 rounded-full border border-dashed transition-colors duration-300',
                isDark ? 'border-white/15' : 'border-neutral-300'
              ]"
            ></div>

            <!-- Middle Orbit Ring -->
            <div
              :class="[
                'absolute w-[64%] h-[64%] rounded-full border transition-colors duration-300',
                isDark ? 'border-[#E11D48]/30' : 'border-[#E11D48]/40'
              ]"
            ></div>

            <!-- Inner Pulse Ring -->
            <div
              :class="[
                'absolute w-[34%] h-[34%] rounded-full border-2 border-[#E11D48]',
                isDark ? 'bg-neutral-950' : 'bg-white'
              ]"
            ></div>

            <!-- Center Hub (Displays Hovered/Selected Tech or Stack Count) -->
            <div class="relative z-20 flex flex-col items-center justify-center text-center p-4 w-32 h-32 sm:w-36 sm:h-36 rounded-full">
              <template v-if="activeSkill">
                <img
                  :src="activeSkill.logo"
                  :alt="activeSkill.name"
                  :class="[
                    'w-10 h-10 sm:w-12 sm:h-12 object-contain mb-1.5 transition-transform duration-200',
                    activeSkill.invertOnDark && isDark ? 'invert' : ''
                  ]"
                />
                <span :class="['font-outfit font-bold text-xs sm:text-sm leading-tight', isDark ? 'text-white' : 'text-neutral-900']">
                  {{ activeSkill.name }}
                </span>
                <span class="text-[10px] font-inter font-semibold uppercase tracking-wider text-[#E11D48] mt-0.5">
                  {{ activeSkill.categoryName }}
                </span>
              </template>
              <template v-else>
                <span class="font-outfit font-black text-2xl sm:text-3xl text-[#E11D48]">
                  {{ allSkills.length }}
                </span>
                <span :class="['font-inter font-semibold text-[11px] uppercase tracking-wider mt-0.5', isDark ? 'text-neutral-300' : 'text-neutral-700']">
                  Tech & Outils
                </span>
              </template>
            </div>

            <!-- Outer Orbiting Nodes (12 items) -->
            <div class="orbit-outer absolute inset-0">
              <div
                v-for="(skill, index) in outerOrbitSkills"
                :key="skill.name"
                class="orbit-node-wrapper"
                :style="getOrbitPosition(index, outerOrbitSkills.length, 50)"
              >
                <button
                  type="button"
                  @mouseenter="activeSkill = skill"
                  @focus="activeSkill = skill"
                  @click="activeSkill = skill"
                  :class="[
                    'orbit-counter-outer w-12 h-12 sm:w-14 sm:h-14 rounded-full border-2 flex items-center justify-center p-2.5 transition-all duration-200 cursor-pointer',
                    activeSkill?.name === skill.name
                      ? 'border-[#E11D48] bg-[#E11D48] scale-125 z-30'
                      : (isDark
                          ? 'bg-neutral-950 border-white/20 hover:border-[#E11D48]'
                          : 'bg-white border-neutral-300 hover:border-[#E11D48]'),
                    activeFilter !== skill.categoryKey ? 'opacity-30' : 'opacity-100'
                  ]"
                  :title="skill.name"
                >
                  <img
                    :src="skill.logo"
                    :alt="skill.name"
                    :class="[
                      'w-full h-full object-contain',
                      (skill.invertOnDark && isDark && activeSkill?.name !== skill.name) ? 'invert' : '',
                      activeSkill?.name === skill.name && skill.invertOnDark ? 'invert' : ''
                    ]"
                  />
                </button>
              </div>
            </div>

            <!-- Inner Orbiting Nodes (9 items, reverse rotation) -->
            <div class="orbit-inner absolute w-[64%] h-[64%]">
              <div
                v-for="(skill, index) in innerOrbitSkills"
                :key="skill.name"
                class="orbit-node-wrapper"
                :style="getOrbitPosition(index, innerOrbitSkills.length, 50)"
              >
                <button
                  type="button"
                  @mouseenter="activeSkill = skill"
                  @focus="activeSkill = skill"
                  @click="activeSkill = skill"
                  :class="[
                    'orbit-counter-inner w-10 h-10 sm:w-12 sm:h-12 rounded-full border-2 flex items-center justify-center p-2 transition-all duration-200 cursor-pointer',
                    activeSkill?.name === skill.name
                      ? 'border-[#E11D48] bg-[#E11D48] scale-125 z-30'
                      : (isDark
                          ? 'bg-neutral-950 border-white/20 hover:border-[#E11D48]'
                          : 'bg-white border-neutral-300 hover:border-[#E11D48]'),
                    activeFilter !== skill.categoryKey ? 'opacity-30' : 'opacity-100'
                  ]"
                  :title="skill.name"
                >
                  <img
                    :src="skill.logo"
                    :alt="skill.name"
                    :class="[
                      'w-full h-full object-contain',
                      (skill.invertOnDark && isDark && activeSkill?.name !== skill.name) ? 'invert' : '',
                      activeSkill?.name === skill.name && skill.invertOnDark ? 'invert' : ''
                    ]"
                  />
                </button>
              </div>
            </div>
          </div>
        </div>

        <!-- Right: Dynamic Circular Badges Grid with Clear Names & Logos -->
        <div class="lg:col-span-6">
          <div class="grid grid-cols-3 sm:grid-cols-4 gap-4 sm:gap-5">
            <button
              v-for="skill in filteredSkills"
              :key="skill.name"
              type="button"
              @mouseenter="activeSkill = skill"
              @focus="activeSkill = skill"
              @click="activeSkill = skill"
              class="group flex flex-col items-center gap-2.5 cursor-pointer text-center focus:outline-none"
            >
              <!-- Circular Pod -->
              <div
                :class="[
                  'relative w-20 h-20 sm:w-24 sm:h-24 rounded-full border-2 flex flex-col items-center justify-center p-4 transition-all duration-200 group-hover:-translate-y-1.5',
                  activeSkill?.name === skill.name
                    ? (isDark
                        ? 'border-[#E11D48] bg-neutral-900 scale-105'
                        : 'border-[#E11D48] bg-neutral-100 scale-105')
                    : (isDark
                        ? 'bg-neutral-950 border-white/15 group-hover:border-[#E11D48]'
                        : 'bg-neutral-50 border-neutral-200 group-hover:border-[#E11D48] group-hover:bg-white')
                ]"
              >
                <!-- Active Red Dot Indicator -->
                <span
                  :class="[
                    'absolute top-1.5 right-1.5 w-2.5 h-2.5 rounded-full bg-[#E11D48] transition-transform duration-200',
                    activeSkill?.name === skill.name ? 'scale-100' : 'scale-0 group-hover:scale-100'
                  ]"
                ></span>

                <img
                  :src="skill.logo"
                  :alt="skill.name"
                  :class="[
                    'w-9 h-9 sm:w-10 sm:h-10 object-contain transition-transform duration-200 group-hover:scale-110',
                    skill.invertOnDark && isDark ? 'invert' : ''
                  ]"
                  loading="lazy"
                />
              </div>

              <!-- Technology Name -->
              <span
                :class="[
                  'font-inter text-xs sm:text-sm font-semibold transition-colors duration-200',
                  activeSkill?.name === skill.name
                    ? 'text-[#E11D48]'
                    : (isDark ? 'text-neutral-300 group-hover:text-white' : 'text-neutral-700 group-hover:text-neutral-950')
                ]"
              >
                {{ skill.name }}
              </span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useI18n } from 'vue-i18n'

defineProps({ isDark: Boolean })
const { t } = useI18n()

const activeFilter = ref('frontend')

const rawCategories = [
  {
    key: 'frontend',
    skills: [
      { name: 'Vue.js', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/vuejs/vuejs-original.svg' },
      { name: 'React.js', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/react/react-original.svg' },
      { name: 'Angular', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/angular/angular-original.svg' },
      { name: 'JavaScript', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/javascript/javascript-original.svg' },
      { name: 'Tailwind CSS', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/tailwindcss/tailwindcss-original.svg' },
      { name: 'HTML5', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/html5/html5-original.svg' },
      { name: 'CSS3', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/css3/css3-original.svg' },
      { name: 'Bootstrap', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/bootstrap/bootstrap-original.svg' },
    ],
  },
  {
    key: 'backend',
    skills: [
      { name: 'PHP', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/php/php-original.svg' },
      { name: 'Laravel', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/laravel/laravel-original.svg' },
      { name: 'Python', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/python/python-original.svg' },
      { name: 'Java', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/java/java-original.svg' },
    ],
  },
  {
    key: 'database',
    skills: [
      { name: 'MySQL', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/mysql/mysql-original.svg' },
      { name: 'PostgreSQL', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/postgresql/postgresql-original.svg' },
      { name: 'Git', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/git/git-original.svg' },
      { name: 'GitHub', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/github/github-original.svg', invertOnDark: true },
      { name: 'Docker', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/docker/docker-original.svg' },
      { name: 'Figma', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/figma/figma-original.svg' },
      { name: 'Postman', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/postman/postman-original.svg' },
      { name: 'Insomnia', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/insomnia/insomnia-original.svg' },
      { name: 'Trello', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/trello/trello-original.svg' },
      { name: 'WordPress', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/wordpress/wordpress-plain.svg', invertOnDark: true },
    ],
  },
]

const filterTabs = computed(() => [
  { id: 'frontend', label: t('skills.frontend') },
  { id: 'backend', label: t('skills.backend') },
  { id: 'database', label: t('skills.database') },
])

const allSkills = computed(() =>
  rawCategories.flatMap((cat) =>
    cat.skills.map((skill) => ({
      ...skill,
      categoryKey: cat.key,
      categoryName: t(`skills.${cat.key}`),
    }))
  )
)

const filteredSkills = computed(() =>
  allSkills.value.filter((s) => s.categoryKey === activeFilter.value)
)

const outerOrbitSkills = computed(() => allSkills.value.slice(0, 12))
const innerOrbitSkills = computed(() => allSkills.value.slice(12))

const activeSkill = ref(null)

function getOrbitPosition(index, total, radiusPercent) {
  const angle = (index / total) * 2 * Math.PI - Math.PI / 2
  const x = 50 + radiusPercent * Math.cos(angle)
  const y = 50 + radiusPercent * Math.sin(angle)
  return {
    left: `${x}%`,
    top: `${y}%`,
  }
}
</script>

<style scoped>
.orbit-node-wrapper {
  position: absolute;
  transform: translate(-50%, -50%);
}

@keyframes spinClockwise {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

@keyframes spinCounterClockwise {
  from {
    transform: rotate(360deg);
  }
  to {
    transform: rotate(0deg);
  }
}

.orbit-outer {
  animation: spinClockwise 38s linear infinite;
}

.orbit-counter-outer {
  animation: spinCounterClockwise 38s linear infinite;
}

.orbit-inner {
  animation: spinCounterClockwise 28s linear infinite;
}

.orbit-counter-inner {
  animation: spinClockwise 28s linear infinite;
}

.orbit-outer:hover,
.orbit-outer:hover .orbit-counter-outer,
.orbit-inner:hover,
.orbit-inner:hover .orbit-counter-inner {
  animation-play-state: paused;
}

@media (prefers-reduced-motion: reduce) {
  .orbit-outer,
  .orbit-counter-outer,
  .orbit-inner,
  .orbit-counter-inner {
    animation: none;
  }
}
</style>
