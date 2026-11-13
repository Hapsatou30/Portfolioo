<template>
  <div
    :class="[
      'py-5 border-y overflow-hidden select-none transition-colors duration-300',
      isDark ? 'bg-[#0a0a0a] border-white/10' : 'bg-neutral-50 border-neutral-200'
    ]"
    aria-label="Technologies marquee"
  >
    <div class="marquee-track flex items-center w-max">
      <div
        v-for="loop in 2"
        :key="loop"
        class="flex items-center shrink-0"
        :aria-hidden="loop === 2 ? 'true' : undefined"
      >
        <div
          v-for="tech in techs"
          :key="`${loop}-${tech.name}`"
          class="flex items-center gap-3 px-6"
        >
          <img
            :src="tech.logo"
            :alt="tech.name"
            class="w-5 h-5 object-contain shrink-0"
            loading="lazy"
          />
          <span
            :class="[
              'font-mono text-sm font-medium tracking-wide whitespace-nowrap',
              isDark ? 'text-neutral-300' : 'text-neutral-700'
            ]"
          >
            {{ tech.name }}
          </span>
          <span class="text-[#E11D48] font-bold ml-6" aria-hidden="true">·</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({ isDark: Boolean })

const techs = [
  { name: 'Vue.js', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/vuejs/vuejs-original.svg' },
  { name: 'React.js', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/react/react-original.svg' },
  { name: 'Angular', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/angular/angular-original.svg' },
  { name: 'JavaScript', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/javascript/javascript-original.svg' },
  { name: 'Tailwind CSS', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/tailwindcss/tailwindcss-original.svg' },
  { name: 'HTML5', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/html5/html5-original.svg' },
  { name: 'CSS3', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/css3/css3-original.svg' },
  { name: 'Laravel', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/laravel/laravel-original.svg' },
  { name: 'PHP', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/php/php-original.svg' },
  { name: 'Python', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/python/python-original.svg' },
  { name: 'Java', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/java/java-original.svg' },
  { name: 'MySQL', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/mysql/mysql-original.svg' },
  { name: 'PostgreSQL', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/postgresql/postgresql-original.svg' },
  { name: 'Docker', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/docker/docker-original.svg' },
  { name: 'Git', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/git/git-original.svg' },
  { name: 'Figma', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/figma/figma-original.svg' },
  { name: 'Postman', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/postman/postman-original.svg' },
  { name: 'Insomnia', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/insomnia/insomnia-original.svg' },
  { name: 'Trello', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/trello/trello-original.svg' },
]
</script>

<style scoped>
@keyframes marqueeScroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

.marquee-track {
  animation: marqueeScroll 32s linear infinite;
}

.marquee-track:hover {
  animation-play-state: paused;
}

@media (prefers-reduced-motion: reduce) {
  .marquee-track {
    animation-duration: 90s;
  }
}
</style>
