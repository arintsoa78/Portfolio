<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Projects from './components/Projects.vue'
import Contact from './components/Contact.vue' // Ton formulaire de contact est actuellement dans Hero.vue

// Gestion du bouton "Retour en haut"
const showScrollTop = ref(false)

const handleScroll = () => {
  showScrollTop.value = window.scrollY > 400
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

const currentYear = new Date().getFullYear()
</script>

<template>
  <div class="app-container">
    <!-- Navbar -->
    <Navbar />

    <!-- Main Content -->
    <main class="main-content">
      <!-- Section Accueil / Hero -->
      <section id="hero" class="section-wrapper">
        <Hero />
      </section>

      <!-- Section À propos -->
      <section id="about" class="section-wrapper">
        <About />
      </section>

      <!-- Section Compétences -->
      <section id="skills" class="section-wrapper">
        <Skills />
      </section>

      <!-- Section Projets -->
      <section id="projects" class="section-wrapper">
        <Projects />
      </section>
      <section id="contact" class="section-wrapper"><Contact /></section>
    </main>

    <!-- Footer -->
    <footer class="footer">
      <div class="footer-content">
        <p>&copy; {{ currentYear }} HARIMANANTSOA Tsiresy Espérencia — Tous droits réservés.</p>
      </div>
    </footer>

    <!-- Bouton Scroll Top -->
    <transition name="fade">
      <button 
        v-if="showScrollTop" 
        @click="scrollToTop" 
        class="scroll-top-btn" 
        aria-label="Retourner en haut"
      >
        <i class="fa-solid fa-arrow-up"></i>
      </button>
    </transition>
  </div>
</template>

<style>
*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
  scroll-padding-top: 80px;
}

body {
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
  background-color: #0f172a;
  color: #f8fafc;
  line-height: 1.6;
  overflow-x: hidden;
}

.app-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.main-content {
  flex: 1;
  max-width: 1200px;
  width: 100%;
  margin: 0 auto;
  padding: 80px 20px 40px;
}

.section-wrapper {
  padding: 40px 0;
}

/* Footer */
.footer {
  border-top: 1px solid rgba(255, 255, 255, 0.05);
  background-color: rgba(15, 23, 42, 0.95);
  padding: 25px 20px;
  text-align: center;
  margin-top: 60px;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 8px;
  color: #94a3b8;
  font-size: 0.9rem;
}

.heart-icon {
  color: #ef4444;
  margin: 0 3px;
}

/* Bouton Scroll Top */
.scroll-top-btn {
  position: fixed;
  bottom: 30px;
  right: 30px;
  width: 45px;
  height: 45px;
  border-radius: 12px;
  background-color: #38bdf8;
  color: #0f172a;
  border: none;
  font-size: 1.1rem;
  font-weight: bold;
  cursor: pointer;
  box-shadow: 0 10px 25px rgba(56, 189, 248, 0.3);
  transition: all 0.3s ease;
  z-index: 99;
  display: flex;
  align-items: center;
  justify-content: center;
}

.scroll-top-btn:hover {
  transform: translateY(-5px);
  background-color: #7dd3fc;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>