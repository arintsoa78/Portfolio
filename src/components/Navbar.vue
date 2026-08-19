<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isMenuOpen = ref(false)
const isScrolled = ref(false)

const navLinks = [
  { name: 'Accueil', href: '#hero' },
  { name: 'À propos', href: '#about' },
  { name: 'Compétences', href: '#skills' },
  { name: 'Projets', href: '#projects' },
  { name: 'Contact', href: '#contact' }
]

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <header
    class="fixed top-0 left-0 z-[1000] w-full transition-all duration-300"
    :class="isScrolled
      ? 'border-b border-white/5 bg-navy/85 py-3.5 shadow-[0_4px_20px_rgb(0_0_0_/_0.3)] backdrop-blur-md'
      : 'bg-transparent py-5'"
  >
    <div class="mx-auto flex max-w-6xl items-center justify-between px-6">
      <a href="#hero" class="group flex flex-col no-underline" @click="closeMenu">
        <span class="text-lg font-bold tracking-wide text-light">
          Espérencia<span class="text-neon">.</span>
        </span>
        <span class="text-[0.7rem] font-medium tracking-[0.14em] text-slate-400 uppercase transition group-hover:text-neon">
          SysAdmin &amp; Réseaux
        </span>
      </a>

      <nav
        class="max-md:fixed max-md:top-0 max-md:z-[1000] max-md:flex max-md:h-screen max-md:w-3/4 max-md:max-w-xs max-md:items-center max-md:justify-center max-md:bg-card/98 max-md:shadow-[-10px_0_30px_rgb(0_0_0_/_0.5)] max-md:backdrop-blur-lg max-md:transition-[right] max-md:duration-300"
        :class="isMenuOpen ? 'max-md:right-0' : 'max-md:-right-full'"
      >
        <ul class="flex list-none flex-col items-center gap-8 p-0 m-0 md:flex-row md:gap-8">
          <li v-for="link in navLinks" :key="link.href">
            <a
              :href="link.href"
              class="relative text-lg font-medium text-slate-300 no-underline transition hover:text-neon after:absolute after:-bottom-1 after:left-0 after:h-0.5 after:w-0 after:bg-neon after:transition-all after:duration-300 hover:after:w-full md:text-[0.95rem]"
              @click="closeMenu"
            >
              {{ link.name }}
            </a>
          </li>
        </ul>
      </nav>

      <button
        type="button"
        class="relative z-[1001] flex h-5 w-7 flex-col justify-between border-0 bg-transparent p-0 md:hidden"
        :aria-expanded="isMenuOpen"
        aria-label="Ouvrir ou fermer le menu de navigation"
        @click="toggleMenu"
      >
        <span
          class="h-0.5 w-full rounded-sm bg-light transition"
          :class="isMenuOpen && 'translate-y-[9px] rotate-45'"
        />
        <span
          class="h-0.5 w-full rounded-sm bg-light transition"
          :class="isMenuOpen && 'opacity-0'"
        />
        <span
          class="h-0.5 w-full rounded-sm bg-light transition"
          :class="isMenuOpen && '-translate-y-[9px] -rotate-45'"
        />
      </button>
    </div>
  </header>
</template>
