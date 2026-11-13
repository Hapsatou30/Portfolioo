<template>
  <div
    :class="[
      'min-h-dvh font-inter transition-colors duration-300',
      isDark ? 'dark bg-[#0a0a0a] text-white' : 'bg-white text-neutral-900'
    ]"
  >
    <!-- Navigation -->
    <NavBar
      :is-dark="isDark"
      :active-section="activeSection"
      @scroll-to="scrollTo"
    />

    <!-- Sections -->
    <main>
      <AboutSection
        :is-dark="isDark"
        @scroll-to="scrollTo"
        @set-dark="setDark"
      />
      <TechMarquee :is-dark="isDark" />
      <SkillsSection :is-dark="isDark" />
      <ExperienceSection :is-dark="isDark" />
      <ProjectsSection :is-dark="isDark" />
      <ContactSection :is-dark="isDark" />
    </main>

    <!-- Footer -->
    <footer
      :class="[
        'py-8 border-t',
        isDark ? 'bg-[#0a0a0a] border-white/10' : 'bg-white border-neutral-200'
      ]"
    >
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex flex-col sm:flex-row items-center justify-between gap-4">
          <div class="flex items-center gap-3">
            <span class="font-outfit text-lg font-bold tracking-tight" :class="isDark ? 'text-white' : 'text-neutral-900'">
              Hapsatou Thiam
            </span>
            <span :class="['font-inter text-sm', isDark ? 'text-neutral-400' : 'text-neutral-600']">
              © {{ new Date().getFullYear() }} {{ $t('footer.rights') }}
            </span>
          </div>
          <div :class="['font-inter text-sm flex items-center gap-1', isDark ? 'text-neutral-400' : 'text-neutral-600']">
            {{ $t('footer.made_with') }} <span class="text-[#E11D48] mx-1">♥</span> {{ $t('footer.by') }}
          </div>
        </div>
      </div>
    </footer>

    <!-- Back to top button -->
    <Transition name="fade">
      <button
        v-if="showBackToTop"
        @click="scrollTo('about')"
        class="fixed bottom-6 right-6 w-11 h-11 rounded-lg bg-[#E11D48] hover:bg-[#BE123C] text-white flex items-center justify-center transition-colors duration-200 z-50 cursor-pointer"
        title="Back to top"
      >
        ↑
      </button>
    </Transition>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import NavBar from './components/NavBar.vue'
import AboutSection from './components/AboutSection.vue'
import TechMarquee from './components/TechMarquee.vue'
import SkillsSection from './components/SkillsSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'

// Dark mode
const isDark = ref(true)

function applyThemeMeta(dark) {
  const meta = document.querySelector('meta[name="color-scheme"]')
  if (meta) {
    meta.content = dark ? 'dark' : 'light'
  }
  document.documentElement.classList.toggle('dark', dark)
}

function setDark(val) {
  isDark.value = val
  localStorage.setItem('portfolio-theme', val ? 'dark' : 'light')
  applyThemeMeta(val)
}

// Active section tracking
const activeSection = ref('about')
const showBackToTop = ref(false)

const sections = ['about', 'skills', 'experience', 'projects', 'contact']

function scrollTo(id) {
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}

function handleScroll() {
  const scrollY = window.scrollY
  showBackToTop.value = scrollY > 400

  for (const section of sections) {
    const el = document.getElementById(section)
    if (el) {
      const rect = el.getBoundingClientRect()
      if (rect.top <= 140 && rect.bottom >= 140) {
        activeSection.value = section
        break
      }
    }
  }
}

onMounted(() => {
  const saved = localStorage.getItem('portfolio-theme')
  if (saved) {
    isDark.value = saved === 'dark'
  }
  applyThemeMeta(isDark.value)
  window.addEventListener('scroll', handleScroll, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.25s ease, transform 0.25s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
  transform: scale(0.9);
}
</style>
