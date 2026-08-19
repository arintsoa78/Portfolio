<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Projects from './components/Projects.vue'
import Contact from './components/Contact.vue'

const showScrollTop = ref(false)

const handleScroll = () => {
  showScrollTop.value = window.scrollY > 400
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

const currentYear = new Date().getFullYear()
</script>

<template>
  <div class="flex min-h-screen flex-col bg-navy">
    <Navbar />

    <main class="mx-auto w-full max-w-6xl flex-1 px-5 pb-10 pt-24">
      <section id="hero" class="py-10">
        <Hero />
      </section>

      <section id="about" class="py-10">
        <About />
      </section>

      <section id="skills" class="py-10">
        <Skills />
      </section>

      <section id="projects" class="py-10">
        <Projects />
      </section>

      <section id="contact" class="py-10">
        <Contact />
      </section>
    </main>

    <footer class="mt-16 border-t border-white/5 bg-navy/95 px-5 py-6 text-center">
      <p class="text-sm text-slate-400">
        &copy; {{ currentYear }} HARIMANANTSOA Tsiresy Espérencia — Tous droits réservés.
      </p>
    </footer>

    <Transition
      enter-active-class="transition-opacity duration-300"
      leave-active-class="transition-opacity duration-300"
      enter-from-class="opacity-0"
      leave-to-class="opacity-0"
    >
      <button
        v-if="showScrollTop"
        type="button"
        class="fixed bottom-7 right-7 z-[99] flex h-11 w-11 items-center justify-center rounded-xl bg-neon text-navy shadow-[0_10px_25px_rgb(56_189_248_/_0.3)] transition hover:-translate-y-1 hover:bg-sky-300"
        aria-label="Retourner en haut"
        @click="scrollToTop"
      >
        <i class="fa-solid fa-arrow-up"></i>
      </button>
    </Transition>
  </div>
</template>
