<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isMenuOpen = ref(false)
const isScrolled = ref(false)

// Liens de navigation
const navLinks = [
  { name: 'Accueil', href: '#hero' },
  { name: 'À propos', href: '#about' },
  { name: 'Compétences', href: '#skills' },
  { name: 'Projets', href: '#projects' },
  { name: 'Contact', href: '#contact' }
]

// Basculer le menu mobile
const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

// Fermer le menu lors du clic sur un lien
const closeMenu = () => {
  isMenuOpen.value = false
}

// Effet d'arrière-plan au défilement (scroll)
const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <header class="navbar-header" :class="{ 'scrolled': isScrolled }">
    <div class="navbar-container">
      <!-- Logo / Mon Nom -->
      <a href="#" class="logo">
        <span class="logo-text">Portfolio</span>
        <span class="dot">.</span>
      </a>

      <!-- Menu de navigation (Desktop) -->
      <nav class="nav-links" :class="{ 'active': isMenuOpen }">
        <ul>
          <li v-for="(link, index) in navLinks" :key="index">
            <a :href="link.href" @click="closeMenu">{{ link.name }}</a>
          </li>
        </ul>
      </nav>

      <!-- Bouton Menu Hamburger (Mobile) -->
      <button 
        class="hamburger" 
        :class="{ 'active': isMenuOpen }" 
        @click="toggleMenu" 
        aria-label="Toggle navigation"
      >
        <span class="bar"></span>
        <span class="bar"></span>
        <span class="bar"></span>
      </button>
    </div>
  </header>
</template>

<style scoped>
.navbar-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  padding: 20px 0;
  transition: all 0.3s ease;
  background-color: transparent;
}

/* Style de la navbar lors du scroll */
.navbar-header.scrolled {
  background-color: rgba(15, 23, 42, 0.85);
  backdrop-filter: blur(12px);
  padding: 15px 0;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.navbar-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 25px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Logo */
.logo {
  font-size: 1.5rem;
  font-weight: 700;
  color: #f8fafc;
  text-decoration: none;
  letter-spacing: 0.5px;
}

.logo .dot {
  color: #38bdf8;
}

/* Navigation Desktop */
.nav-links ul {
  display: flex;
  list-style: none;
  gap: 30px;
  margin: 0;
  padding: 0;
}

.nav-links a {
  color: #cbd5e1;
  text-decoration: none;
  font-size: 0.95rem;
  font-weight: 500;
  transition: color 0.3s ease;
  position: relative;
}

.nav-links a:hover {
  color: #38bdf8;
}

/* Soulignement animé au survol */
.nav-links a::after {
  content: '';
  position: absolute;
  width: 0;
  height: 2px;
  bottom: -4px;
  left: 0;
  background-color: #38bdf8;
  transition: width 0.3s ease;
}

.nav-links a:hover::after {
  width: 100%;
}

/* Menu Hamburger (Mobile) */
.hamburger {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 28px;
  height: 20px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
  z-index: 1001;
}

.hamburger .bar {
  height: 3px;
  width: 100%;
  background-color: #f8fafc;
  border-radius: 2px;
  transition: all 0.3s ease;
}

/* Animation Hamburger -> Croix */
.hamburger.active .bar:nth-child(1) {
  transform: translateY(8.5px) rotate(45deg);
}

.hamburger.active .bar:nth-child(2) {
  opacity: 0;
}

.hamburger.active .bar:nth-child(3) {
  transform: translateY(-8.5px) rotate(-45deg);
}

/* Responsive Styles (Mobile & Tablette) */
@media (max-width: 768px) {
  .hamburger {
    display: flex;
  }

  .nav-links {
    position: fixed;
    top: 0;
    right: -100%;
    width: 75%;
    max-width: 300px;
    height: 100vh;
    background-color: rgba(30, 41, 59, 0.98);
    backdrop-filter: blur(15px);
    box-shadow: -10px 0 30px rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    transition: right 0.4s ease;
  }

  .nav-links.active {
    right: 0;
  }

  .nav-links ul {
    flex-direction: column;
    align-items: center;
    gap: 30px;
  }

  .nav-links a {
    font-size: 1.2rem;
  }
}
</style>