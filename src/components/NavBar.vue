<template>
  <header
    :class="[
      'fixed top-0 left-0 right-0 z-50 transition-colors duration-300 border-b',
      isDark
        ? 'bg-[#0a0a0a]/95 border-white/10 text-white'
        : 'bg-white/95 border-neutral-200 text-neutral-900'
    ]"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-20">
        <!-- Brand / Logo -->
        <button
          type="button"
          class="font-outfit text-lg sm:text-xl font-bold tracking-tight cursor-pointer text-left"
          :class="isDark ? 'text-white' : 'text-neutral-900'"
          @click="$emit('scroll-to', 'about')"
        >
          Hapsatou Thiam
        </button>

        <!-- Desktop Navigation -->
        <nav aria-label="Main navigation" class="hidden md:flex items-center gap-8">
          <button
            v-for="item in navItems"
            :key="item.key"
            type="button"
            @click="$emit('scroll-to', item.target)"
            :aria-current="activeSection === item.target ? 'page' : undefined"
            :class="[
              'nav-link font-inter text-sm font-medium transition-colors duration-200 cursor-pointer py-1',
              activeSection === item.target
                ? 'text-[#E11D48] font-semibold active'
                : (isDark ? 'text-neutral-400 hover:text-white' : 'text-neutral-600 hover:text-neutral-900')
            ]"
          >
            {{ $t(`nav.${item.key}`) }}
          </button>
        </nav>

        <!-- Right CTA & Mobile Menu Toggle -->
        <div class="flex items-center gap-3">
          <button
            type="button"
            @click="$emit('scroll-to', 'contact')"
            class="px-5 py-2.5 rounded-lg bg-[#E11D48] hover:bg-[#BE123C] text-white font-inter text-sm font-semibold transition-colors duration-200 cursor-pointer"
          >
            {{ $t('nav.hire_me') }}
          </button>

          <!-- Mobile menu button -->
          <button
            type="button"
            class="md:hidden w-10 h-10 rounded-lg border flex flex-col items-center justify-center gap-1.5 transition-colors duration-200 cursor-pointer"
            :class="isDark ? 'border-white/15 text-white hover:bg-white/5' : 'border-neutral-300 text-neutral-900 hover:bg-neutral-100'"
            @click="mobileOpen = !mobileOpen"
            aria-label="Toggle navigation menu"
          >
            <span :class="['w-4 h-0.5 transition-transform duration-200', isDark ? 'bg-white' : 'bg-neutral-900', mobileOpen ? 'rotate-45 translate-y-2' : '']"></span>
            <span :class="['w-4 h-0.5 transition-opacity duration-200', isDark ? 'bg-white' : 'bg-neutral-900', mobileOpen ? 'opacity-0' : '']"></span>
            <span :class="['w-4 h-0.5 transition-transform duration-200', isDark ? 'bg-white' : 'bg-neutral-900', mobileOpen ? '-rotate-45 -translate-y-2' : '']"></span>
          </button>
        </div>
      </div>

      <!-- Mobile Menu -->
      <Transition name="mobile-menu">
        <div
          v-if="mobileOpen"
          :class="[
            'md:hidden py-4 pb-6 border-t',
            isDark ? 'border-white/10' : 'border-neutral-200'
          ]"
        >
          <div class="flex flex-col gap-3">
            <button
              v-for="item in navItems"
              :key="item.key"
              type="button"
              @click="$emit('scroll-to', item.target); mobileOpen = false"
              :class="[
                'text-left font-inter font-medium text-sm transition-colors duration-200 px-2 py-1.5 rounded-md cursor-pointer',
                activeSection === item.target
                  ? 'text-[#E11D48] font-semibold'
                  : (isDark ? 'text-neutral-300 hover:text-white' : 'text-neutral-700 hover:text-neutral-900')
              ]"
            >
              {{ $t(`nav.${item.key}`) }}
            </button>
          </div>
        </div>
      </Transition>
    </div>
  </header>
</template>

<script setup>
import { ref } from 'vue'

defineProps({
  isDark: Boolean,
  activeSection: String,
})

defineEmits(['scroll-to'])

const mobileOpen = ref(false)

const navItems = [
  { key: 'about', target: 'about' },
  { key: 'skills', target: 'skills' },
  { key: 'experience', target: 'experience' },
  { key: 'projects', target: 'projects' },
  { key: 'contact', target: 'contact' },
]
</script>

<style scoped>
.mobile-menu-enter-active,
.mobile-menu-leave-active {
  transition: opacity 0.2s ease, transform 0.2s ease;
}
.mobile-menu-enter-from,
.mobile-menu-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}
</style>
