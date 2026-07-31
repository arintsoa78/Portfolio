<script setup>
import { ref, computed } from 'vue'

// Catégories de filtres
const categories = ['Tous', 'Réseaux & Systèmes', 'Développement Web', 'Applications']
const activeCategory = ref('Tous')

// Projets basés sur ton CV avec carrousel d'images
const projects = ref([
  {
    id: 1,
    title: 'Conception & Simulation Réseau GNS3',
    category: 'Réseaux & Systèmes',
    description: 'Configuration de routeurs et commutateurs, mise en place du plan d’adressage IPv4, routage RIP/OSPF, tests de connectivité et dépannage réseau.',
    tags: ['GNS3', 'RIP', 'OSPF', 'IPv4', 'Switching'],
    icon: 'fa-solid fa-network-wired',
    github: null,
    currentImageIndex: 0,
    images: [
      { url: '/projects/R1.png', caption: 'Topologie Réseau sous GNS3' },
      { url: '/projects/R2.png', caption: 'Tests de ping & Wireshark' }
    ]
  },
  {
    id: 2,
    title: 'Administration & Maintenance Windows',
    category: 'Réseaux & Systèmes',
    description: 'Assistance à distance via TeamViewer et PsExec, exécution de commandes à distance, maintenance et optimisation de postes de travail.',
    tags: ['Windows', 'PsExec', 'TeamViewer', 'Maintenance'],
    icon: 'fa-solid fa-desktop',
    github: null,
    currentImageIndex: 0,
    images: [
      { url: '/projects/T1.png', caption: 'Connexion à distance par teamViewer' },
      { url: '/projects/T2.png', caption: 'Connexion à distance par teamViewer' },
      { url: '/projects/T3.png', caption: 'Console de maintenance Windows' }
    ]
  },
  {
    id: 3,
    title: 'Virtualisation sous VMware Workstation',
    category: 'Réseaux & Systèmes',
    description: 'Création, configuration et gestion de machines virtuelles (Linux/Windows) pour des environnements de test et de simulation.',
    tags: ['VMware', 'Virtualisation', 'Linux', 'Windows Server'],
    icon: 'fa-solid fa-server',
    github: null,
    currentImageIndex: 0,
    images: [
      { url: '/projects/c1.png', caption: 'Infrastructure sous VMware Workstation' }
  
    ]
  },
  {
    id: 4,
    title: 'Tableau de bord Médical Interactif',
    category: 'Développement Web',
    description: 'Développement d’une application web de gestion d’un cabinet médical avec interface interactive et dynamique.',
    tags: ['Vue.js', 'React.js', 'JavaScript', 'HTML/CSS'],
    icon: 'fa-solid fa-heart-pulse',
    github: null,
    currentImageIndex: 0,
    images: [
      { url: '/projects/M1.jpeg', caption: 'Dashboard principal du cabinet' },
      { url: '/projects/M2.jpeg', caption: 'Bilan de préstation' },
      { url: '/projects/M3.jpeg', caption: 'Listes des medecins' },
      { url: '/projects/M4.jpeg' }
    ]
  },
  {
    id: 5,
    title: 'Gestion de Vente de Voitures',
    category: 'Développement Web',
    description: 'Conception d’une application web permettant la gestion des clients, des véhicules, des achats et la génération de factures.',
    tags: ['PHP', 'MySQL', 'HTML/CSS', 'DataTables'],
    icon: 'fa-solid fa-car',
    github: null,
    currentImageIndex: 0,
    images: [
      { url: '/projects/gv1.png', caption: 'Login' },
      { url: '/projects/gv2.png', caption: 'Accueil' },
      { url: '/projects/gv3.png', caption: 'Gestion des clients' },
      { url: '/projects/gv4.png', caption: 'Gestion des voitures' },
      { url: '/projects/gv5.png', caption: 'Gestion des achats' },
      { url: '/projects/gv6.png', caption: 'Interface de facturation' },
      { url: '/projects/gv7.png', caption: 'Interface de facturation PHP/MySQL' }
    ]
  },
  {
    id: 6,
    title: 'Gestion de Rendez-vous Cabinet d\'Avocat',
    category: 'Applications',
    description: 'Application Desktop pour la gestion des clients, des avocats, des plannings, des consultations et le suivi des RDV.',
    tags: ['C#', '.NET', 'Base de données'],
    icon: 'fa-solid fa-scale-balanced',
    github: null,
    currentImageIndex: 0,
    images: [
      { url: '/projects/A3.jpeg', caption: 'Login' },
      { url: '/projects/A1.jpeg', caption: 'Demandes de rendez-vouz sur le côté avocats' },
      { url: '/projects/A2.jpeg', caption: 'Gestion des fiches clients' }  
    ]
  },
])

// Filtrage dynamique
const filteredProjects = computed(() => {
  if (activeCategory.value === 'Tous') {
    return projects.value
  }
  return projects.value.filter(p => p.category === activeCategory.value)
})

// Navigation dans le carrousel
const nextImage = (project) => {
  if (project.currentImageIndex < project.images.length - 1) {
    project.currentImageIndex++
  } else {
    project.currentImageIndex = 0
  }
}

const prevImage = (project) => {
  if (project.currentImageIndex > 0) {
    project.currentImageIndex--
  } else {
    project.currentImageIndex = project.images.length - 1
  }
}

const setImage = (project, index) => {
  project.currentImageIndex = index
}
</script>

<template>
  <section class="projects-section" id="projects">
    <!-- En-tête -->
    <div class="section-title">
      <h2>Projets <span>Académiques</span></h2>
      <div class="underline"></div>
      <p class="subtitle">
        Projets et travaux pratiques réalisés durant mon parcours à l'École Nationale d'Informatique (ENI).
      </p>
    </div>

    <!-- Boutons de Filtrage -->
    <div class="filter-container">
      <button 
        v-for="cat in categories" 
        :key="cat"
        class="filter-btn"
        :class="{ active: activeCategory === cat }"
        @click="activeCategory = cat"
      >
        {{ cat }}
      </button>
    </div>

    <!-- Grille des Projets -->
    <div class="projects-grid">
      <div 
        v-for="project in filteredProjects" 
        :key="project.id" 
        class="project-card"
      >
        <!-- CARROUSEL D'IMAGES -->
        <div class="carousel-container">
          <div class="carousel-slide">
            <img 
              :src="project.images[project.currentImageIndex].url" 
              :alt="project.images[project.currentImageIndex].caption"
              class="carousel-image"

            />
            <span class="carousel-caption">
              {{ project.images[project.currentImageIndex].caption }}
            </span>
          </div>

          <!-- Contrôles du Carrousel (visibles uniquement s'il y a plus d'une image) -->
          <template v-if="project.images.length > 1">
            <button @click="prevImage(project)" class="nav-btn prev-btn" aria-label="Précédent">
              <i class="fa-solid fa-chevron-left"></i>
            </button>
            <button @click="nextImage(project)" class="nav-btn next-btn" aria-label="Suivant">
              <i class="fa-solid fa-chevron-right"></i>
            </button>

            <!-- Puces indicateurs -->
            <div class="carousel-dots">
              <span 
                v-for="(img, idx) in project.images" 
                :key="idx"
                class="dot"
                :class="{ active: idx === project.currentImageIndex }"
                @click="setImage(project, idx)"
              ></span>
            </div>
          </template>

          <span class="category-tag">{{ project.category }}</span>
        </div>

        <!-- EN-TÊTE & DÉTAILS DE LA CARTE -->
        <div class="card-content">
          <div class="card-header">
            <div class="icon-box">
              <i :class="project.icon"></i>
            </div>
            <h3>{{ project.title }}</h3>
          </div>

          <p class="description">{{ project.description }}</p>

          <div class="card-footer">
            <div class="tags">
              <span v-for="tag in project.tags" :key="tag" class="tag">
                {{ tag }}
              </span>
            </div>

            <div class="project-links" v-if="project.github">
              <a :href="project.github" target="_blank" rel="noopener noreferrer" title="Voir sur GitHub">
                <i class="fa-brands fa-github"></i>
              </a>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
.projects-section {
  padding: 60px 0;
}

/* Titre de section */
.section-title {
  text-align: center;
  margin-bottom: 40px;
}

.section-title h2 {
  font-size: 2.2rem;
  font-weight: 700;
  color: #f8fafc;
}

.section-title h2 span {
  color: #38bdf8;
}

.underline {
  width: 60px;
  height: 4px;
  background: linear-gradient(90deg, #38bdf8, #3b82f6);
  margin: 10px auto 0;
  border-radius: 2px;
}

.subtitle {
  color: #94a3b8;
  margin-top: 15px;
  font-size: 1.05rem;
  max-width: 650px;
  margin-left: auto;
  margin-right: auto;
}

/* Filtres */
.filter-container {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-bottom: 40px;
  flex-wrap: wrap;
}

.filter-btn {
  background-color: rgba(30, 41, 59, 0.6);
  color: #94a3b8;
  border: 1px solid rgba(255, 255, 255, 0.08);
  padding: 8px 18px;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
}

.filter-btn:hover {
  color: #f8fafc;
  border-color: rgba(56, 189, 248, 0.4);
}

.filter-btn.active {
  background-color: #38bdf8;
  color: #0f172a;
  border-color: #38bdf8;
  font-weight: 600;
}

/* Grille */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(330px, 1fr));
  gap: 30px;
}

/* Carte Projet */
.project-card {
  background-color: rgba(30, 41, 59, 0.7);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 16px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  transition: transform 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
}

.project-card:hover {
  transform: translateY(-5px);
  border-color: rgba(56, 189, 248, 0.4);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.35);
}

/* Styles du Carrousel */
.carousel-container {
  position: relative;
  width: 100%;
  height: 200px;
  background-color: #0f172a;
  overflow: hidden;
}

.carousel-slide {
  position: relative;
  width: 100%;
  height: 100%;
}

.carousel-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: opacity 0.3s ease;
}

.carousel-caption {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(0deg, rgba(15, 23, 42, 0.95) 0%, rgba(15, 23, 42, 0) 100%);
  color: #f8fafc;
  padding: 10px 12px 22px;
  font-size: 0.78rem;
  font-weight: 500;
}

/* Navigation Flèches */
.nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(15, 23, 42, 0.75);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: #f8fafc;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.2s ease;
  opacity: 0.6;
}

.carousel-container:hover .nav-btn {
  opacity: 1;
}

.nav-btn:hover {
  background-color: #38bdf8;
  color: #0f172a;
}

.prev-btn { left: 8px; }
.next-btn { right: 8px; }

/* Indicateurs Puces */
.carousel-dots {
  position: absolute;
  bottom: 6px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 5px;
  z-index: 2;
}

.dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.35);
  cursor: pointer;
  transition: all 0.3s ease;
}

.dot.active {
  background-color: #38bdf8;
  width: 16px;
  border-radius: 10px;
}

.category-tag {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 0.7rem;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  color: #38bdf8;
  background-color: rgba(15, 23, 42, 0.85);
  border: 1px solid rgba(56, 189, 248, 0.3);
  padding: 4px 10px;
  border-radius: 6px;
  font-weight: 600;
}

/* Contenu de la Carte */
.card-content {
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  flex-grow: 1;
}

.card-header {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 12px;
}

.icon-box {
  width: 38px;
  height: 38px;
  background-color: rgba(56, 189, 248, 0.1);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.icon-box i {
  color: #38bdf8;
  font-size: 1.1rem;
}

.card-header h3 {
  font-size: 1.1rem;
  color: #f8fafc;
  line-height: 1.3;
}

.description {
  color: #cbd5e1;
  font-size: 0.88rem;
  line-height: 1.55;
  margin-bottom: 20px;
}

/* Footer Carte */
.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  gap: 10px;
  margin-top: auto;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.tag {
  font-size: 0.72rem;
  color: #94a3b8;
  background-color: rgba(15, 23, 42, 0.6);
  padding: 3px 8px;
  border-radius: 4px;
}

.project-links a {
  color: #cbd5e1;
  font-size: 1.2rem;
  transition: color 0.3s ease;
}

.project-links a:hover {
  color: #38bdf8;
}

@media (max-width: 640px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>