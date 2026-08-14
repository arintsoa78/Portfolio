<script setup>
import { ref, onMounted } from 'vue'

const personalInfo = {
  name: 'HARIMANANTSOA Tsiresy Espérencia',
  subtitles: [
    'Étudiante en L2 Informatique',
    'Administratrice Systèmes & Réseaux',
    'Passionnée de Cybersécurité'
  ],
  bio: 'Actuellement en recherche d\'un stage. Je conçois, simule et sécurise des infrastructures réseaux complexes (GNS3, Cisco, Windows Server) tout en développant mes compétences sur Linux.',
  location: 'Antananarivo',
  email: 'anaharintsoa@gmail.com',
  phone: '+261 33 40 183 14'
}

// Effet "Texte Tapé" (Typewriter effect)
const currentSubtitleIndex = ref(0)
const currentText = ref('')
const isDeleting = ref(false)

const typeEffect = () => {
  const fullText = personalInfo.subtitles[currentSubtitleIndex.value]
  
  if (isDeleting.value) {
    currentText.value = fullText.substring(0, currentText.value.length - 1)
  } else {
    currentText.value = fullText.substring(0, currentText.value.length + 1)
  }

  let typeSpeed = isDeleting.value ? 50 : 100

  if (!isDeleting.value && currentText.value === fullText) {
    typeSpeed = 2000 // Pause à la fin du mot
    isDeleting.value = true
  } else if (isDeleting.value && currentText.value === '') {
    isDeleting.value = false
    currentSubtitleIndex.value = (currentSubtitleIndex.value + 1) % personalInfo.subtitles.length
    typeSpeed = 500
  }

  setTimeout(typeEffect, typeSpeed)
}

onMounted(() => {
  typeEffect()
})

const stats = [
  { icon: 'fa-solid fa-graduation-cap', label: 'Niveau', value: 'Licence 2' },
  { icon: 'fa-solid fa-network-wired', label: 'Spécialité', value: 'Systèmes & Réseaux' },
  { icon: 'fa-solid fa-briefcase', label: 'Objectif', value: 'Stage Pro' }
]

const socialLinks = [
  { icon: 'fa-brands fa-linkedin-in', href: 'https://linkedin.com', label: 'LinkedIn' },
  { icon: 'fa-brands fa-github', href: 'https://github.com/arintsoa78', label: 'GitHub' }
]
</script>

<template>
  <section class="hero-section" id="hero">
    <!-- Décoration d'arrière-plan animée -->
    <div class="bg-glow glow-1"></div>
    <div class="bg-glow glow-2"></div>

    <div class="hero-grid">
      <!-- Colonne Présentation Texte -->
      <div class="hero-text-wrapper">
        <div class="status-badge">
          <span class="ping-dot"></span>
          <span>Disponible pour un stage</span>
        </div>

        <h1 class="hero-title">
          Bonjour, je suis <br />
          <span class="gradient-text">{{ personalInfo.name }}</span>
        </h1>

        <!-- Sous-titre animé -->
        <div class="typewriter-container">
          <span class="typewriter-text">{{ currentText }}</span>
          <span class="cursor">|</span>
        </div>

        <p class="hero-bio">
          {{ personalInfo.bio }}
        </p>

        <!-- Statistiques / Cartes rapides -->
        <div class="stats-cards">
          <div v-for="(stat, index) in stats" :key="index" class="stat-card">
            <i :class="stat.icon"></i>
            <div>
              <span class="stat-value">{{ stat.value }}</span>
              <span class="stat-label">{{ stat.label }}</span>
            </div>
          </div>
        </div>

        <!-- Boutons d'action -->
        <div class="hero-actions">
          <a href="#projects" class="btn btn-primary">
            <span>Découvrir mes projets</span>
            <i class="fa-solid fa-arrow-right"></i>
          </a>
          <a href="#contact" class="btn btn-outline">
            <span>Me Contacter</span>
            <i class="fa-solid fa-paper-plane"></i>
          </a>
          <!-- Bouton Télécharger le CV -->
            <a 
                href="/projects/CV_Esperencia.pdf" 
                download="CV_Esperencian.pdf" 
                class="btn btn-primary"
            >
                <span>Télécharger CV</span>
                <i class="fa-solid fa-download"></i>
            </a>
        </div>

        <!-- Liens sociaux -->
        <div class="social-links">
          <a 
            v-for="(social, index) in socialLinks" 
            :key="index" 
            :href="social.href" 
            target="_blank" 
            rel="noopener noreferrer"
            :aria-label="social.label"
            class="social-btn"
          >
            <i :class="social.icon"></i>
          </a>
        </div>
      </div>

      <!-- Colonne Visuel Animé (Hub Réseau Interactif) -->
      <div class="hero-visual-wrapper">
        <div class="network-orbit">
          <!-- Cercle central -->
          <div class="center-node">
            <i class="fa-solid fa-server"></i>
          </div>

          <!-- Badges flottants en orbite animée -->
          <div class="orbit-item badge-gns3">
            <i class="fa-solid fa-network-wired"></i>
            <span>GNS3</span>
          </div>

          <div class="orbit-item badge-linux">
            <i class="fa-brands fa-linux"></i>
            <span>Linux</span>
          </div>

          <div class="orbit-item badge-windows">
            <i class="fa-brands fa-windows"></i>
            <span>Windows</span>
          </div>

          <div class="orbit-item badge-cisco">
            <i class="fa-solid fa-shield-halved"></i>
            <span>Cisco</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero-section {
  position: relative;
  padding: 80px 0 40px;
  min-height: 85vh;
  display: flex;
  align-items: center;
  overflow: hidden;
}

/* Effet de lueur d'arrière-plan */
.bg-glow {
  position: absolute;
  border-radius: 50%;
  filter: blur(120px);
  z-index: 0;
  opacity: 0.15;
}

.glow-1 {
  width: 350px;
  height: 350px;
  background-color: #38bdf8;
  top: 10%;
  left: -5%;
}

.glow-2 {
  width: 400px;
  height: 400px;
  background-color: #3b82f6;
  bottom: 10%;
  right: -5%;
}

.hero-grid {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  gap: 50px;
  align-items: center;
  width: 100%;
}

/* Badge Statut */
.status-badge {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background-color: rgba(34, 197, 94, 0.1);
  border: 1px solid rgba(34, 197, 94, 0.3);
  padding: 6px 16px;
  border-radius: 20px;
  color: #4ade80;
  font-size: 0.85rem;
  font-weight: 500;
  margin-bottom: 25px;
}

.ping-dot {
  width: 8px;
  height: 8px;
  background-color: #22c55e;
  border-radius: 50%;
  box-shadow: 0 0 0 0 rgba(34, 197, 94, 0.7);
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(34, 197, 94, 0.7); }
  70% { transform: scale(1); box-shadow: 0 0 0 8px rgba(34, 197, 94, 0); }
  100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(34, 197, 94, 0); }
}

/* Titre & Gradient */
.hero-title {
  font-size: 2.8rem;
  font-weight: 800;
  color: #f8fafc;
  line-height: 1.2;
  margin-bottom: 15px;
}

.gradient-text {
  background: linear-gradient(135deg, #38bdf8 0%, #3b82f6 100%);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  color: transparent;
}

/* Effet Typewriter */
.typewriter-container {
  font-size: 1.4rem;
  font-weight: 600;
  color: #cbd5e1;
  min-height: 40px;
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.typewriter-text {
  color: #38bdf8;
}

.cursor {
  animation: blink 0.7s infinite;
  color: #38bdf8;
  margin-left: 2px;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

.hero-bio {
  color: #94a3b8;
  font-size: 1.05rem;
  line-height: 1.7;
  margin-bottom: 30px;
  max-width: 580px;
}

/* Cartes Stats */
.stats-cards {
  display: flex;
  gap: 20px;
  margin-bottom: 35px;
  flex-wrap: wrap;
}

.stat-card {
  display: flex;
  align-items: center;
  gap: 15px;
  background-color: rgba(30, 41, 59, 0.6);
  border: 1px solid rgba(255, 255, 255, 0.05);
  padding: 12px 18px;
  border-radius: 12px;
  backdrop-filter: blur(10px);
}

.stat-card i {
  font-size: 1.3rem;
  color: #38bdf8;
}

.stat-value {
  display: block;
  font-weight: 700;
  color: #f8fafc;
  font-size: 0.95rem;
}

.stat-label {
  font-size: 0.75rem;
  color: #94a3b8;
}

/* Boutons */
.hero-actions {
  display: flex;
  gap: 15px;
  margin-bottom: 30px;
  flex-wrap: wrap;
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 14px 28px;
  border-radius: 10px;
  font-size: 0.95rem;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s ease;
  cursor: pointer;
}

.btn-primary {
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: #ffffff;
  box-shadow: 0 10px 25px -5px rgba(37, 99, 235, 0.4);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 30px -5px rgba(37, 99, 235, 0.6);
}

.btn-outline {
  background-color: rgba(30, 41, 59, 0.8);
  color: #f8fafc;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.btn-outline:hover {
  border-color: #38bdf8;
  color: #38bdf8;
  transform: translateY(-3px);
}

/* Liens Sociaux */
.social-links {
  display: flex;
  gap: 12px;
}

.social-btn {
  width: 42px;
  height: 42px;
  border-radius: 10px;
  background-color: rgba(30, 41, 59, 0.8);
  border: 1px solid rgba(255, 255, 255, 0.08);
  color: #f8fafc;
  display: flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;
  transition: all 0.3s ease;
}

.social-btn:hover {
  background-color: #38bdf8;
  color: #0f172a;
  transform: translateY(-3px);
}

/* Visuel Orbite Animée */
.hero-visual-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}

.network-orbit {
  position: relative;
  width: 300px;
  height: 300px;
  border: 2px dashed rgba(56, 189, 248, 0.2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  animation: rotateOrbit 25s linear infinite;
}

@keyframes rotateOrbit {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.center-node {
  width: 90px;
  height: 90px;
  background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
  border: 2px solid #38bdf8;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 30px rgba(56, 189, 248, 0.3);
  animation: counterRotate 25s linear infinite;
}

.center-node i {
  font-size: 2.2rem;
  color: #38bdf8;
}

.orbit-item {
  position: absolute;
  background-color: rgba(30, 41, 59, 0.9);
  border: 1px solid rgba(56, 189, 248, 0.3);
  padding: 8px 14px;
  border-radius: 20px;
  display: flex;
  align-items: center;
  gap: 8px;
  color: #f8fafc;
  font-size: 0.85rem;
  font-weight: 500;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
  animation: counterRotate 25s linear infinite;
}

@keyframes counterRotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(-360deg); }
}

.orbit-item i {
  color: #38bdf8;
}

/* Positions sur l'orbite */
.badge-gns3 { top: -15px; }
.badge-linux { right: -20px; }
.badge-windows { bottom: -15px; }
.badge-cisco { left: -20px; }

/* Responsive */
@media (max-width: 968px) {
  .hero-grid {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 40px;
  }

  .status-badge, .typewriter-container, .stats-cards, .hero-actions, .social-links {
    justify-content: center;
  }

  .hero-bio {
    margin-left: auto;
    margin-right: auto;
  }

  .hero-title {
    font-size: 2.2rem;
  }

  .network-orbit {
    width: 250px;
    height: 250px;
  }
}
</style>