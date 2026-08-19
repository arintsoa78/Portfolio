<script setup>
import { ref, computed } from 'vue'

const categories = ['Tous', 'Réseaux & Systèmes', 'Développement Web', 'Applications']
const activeCategory = ref('Tous')

const projects = ref([
  {
    id: 1,
    title: 'Conception & Simulation Réseau GNS3',
    category: 'Réseaux & Systèmes',
    description: 'Configuration de routeurs et commutateurs, mise en place du plan d’adressage IPv4, routage RIP/OSPF, tests de connectivité et dépannage réseau.',
    tags: ['GNS3', 'RIP', 'OSPF', 'IPv4', 'Switching'],
    icon: 'fa-solid fa-network-wired',
    currentImageIndex: 0,
    images: [
      { url: '/projects/R1.png', caption: 'Topologie Réseau' },
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
    currentImageIndex: 0,
    images: [
      { url: '/projects/T1.png', caption: 'Connexion à distance par TeamViewer' },
      { url: '/projects/T2.png', caption: 'Connexion à distance par TeamViewer' },
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
    currentImageIndex: 0,
    images: [
      { url: '/projects/M1.jpeg', caption: 'Dashboard principal du cabinet' },
      { url: '/projects/M2.jpeg', caption: 'Bilan de prestation' },
      { url: '/projects/M3.jpeg', caption: 'Liste des médecins' },
      { url: '/projects/M4.jpeg', caption: 'Aperçu de l\'application' }
    ]
  },
  {
    id: 5,
    title: 'Gestion de Vente de Voitures',
    category: 'Développement Web',
    description: 'Conception d’une application web permettant la gestion des clients, des véhicules, des achats et la génération de factures.',
    tags: ['PHP', 'MySQL', 'HTML/CSS', 'DataTables'],
    icon: 'fa-solid fa-car',
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
    currentImageIndex: 0,
    images: [
      { url: '/projects/A3.jpeg', caption: 'Login' },
      { url: '/projects/A1.jpeg', caption: 'Demandes de rendez-vous côté avocat' },
      { url: '/projects/A2.jpeg', caption: 'Gestion des fiches clients' }
    ]
  }
])

const filteredProjects = computed(() => {
  if (activeCategory.value === 'Tous') return projects.value
  return projects.value.filter((p) => p.category === activeCategory.value)
})

const nextImage = (project) => {
  project.currentImageIndex = (project.currentImageIndex + 1) % project.images.length
}

const prevImage = (project) => {
  const total = project.images.length
  project.currentImageIndex = (project.currentImageIndex - 1 + total) % total
}

const setImage = (project, index) => {
  project.currentImageIndex = index
}
</script>

<template>
  <div class="py-6">
    <div class="mb-10 text-center">
      <h2 class="text-[2.2rem] font-bold text-light">
        Projets <span class="text-neon">Académiques</span>
      </h2>
      <div class="mx-auto mt-2.5 h-1 w-15 rounded-sm bg-linear-to-r from-neon to-accent" />
      <p class="mx-auto mt-4 max-w-xl text-[1.05rem] text-slate-400">
        Projets et travaux pratiques réalisés durant mon parcours à l'École Nationale d'Informatique (ENI).
      </p>
    </div>

    <div class="mb-10 flex flex-wrap justify-center gap-3">
      <button
        v-for="cat in categories"
        :key="cat"
        type="button"
        class="rounded-full border px-4.5 py-2 text-sm font-medium transition"
        :class="activeCategory === cat
          ? 'border-neon bg-neon font-semibold text-navy'
          : 'border-white/8 bg-card/60 text-slate-400 hover:border-neon/40 hover:text-light'"
        @click="activeCategory = cat"
      >
        {{ cat }}
      </button>
    </div>

    <div class="grid grid-cols-1 gap-8 sm:grid-cols-2 xl:grid-cols-3">
      <article
        v-for="project in filteredProjects"
        :key="project.id"
        class="flex flex-col overflow-hidden rounded-2xl border border-white/8 bg-card/70 backdrop-blur-md transition hover:-translate-y-1 hover:border-neon/40 hover:shadow-[0_12px_30px_rgb(0_0_0_/_0.35)]"
      >
        <div class="group relative h-50 overflow-hidden bg-navy">
          <img
            :src="project.images[project.currentImageIndex].url"
            :alt="project.images[project.currentImageIndex].caption || project.title"
            class="h-full w-full object-cover"
          />
          <span
            v-if="project.images[project.currentImageIndex].caption"
            class="absolute inset-x-0 bottom-0 bg-linear-to-t from-navy/95 to-transparent px-3 pt-6 pb-6 text-xs font-medium text-light"
          >
            {{ project.images[project.currentImageIndex].caption }}
          </span>

          <template v-if="project.images.length > 1">
            <button
              type="button"
              class="absolute top-1/2 left-2 flex h-8 w-8 -translate-y-1/2 items-center justify-center rounded-full border border-white/10 bg-navy/75 text-light opacity-60 transition hover:bg-neon hover:text-navy group-hover:opacity-100"
              aria-label="Image précédente"
              @click.stop="prevImage(project)"
            >
              <i class="fa-solid fa-chevron-left text-xs"></i>
            </button>
            <button
              type="button"
              class="absolute top-1/2 right-2 flex h-8 w-8 -translate-y-1/2 items-center justify-center rounded-full border border-white/10 bg-navy/75 text-light opacity-60 transition hover:bg-neon hover:text-navy group-hover:opacity-100"
              aria-label="Image suivante"
              @click.stop="nextImage(project)"
            >
              <i class="fa-solid fa-chevron-right text-xs"></i>
            </button>

            <div class="absolute bottom-1.5 left-1/2 z-2 flex -translate-x-1/2 gap-1.5">
              <button
                v-for="(img, idx) in project.images"
                :key="img.url"
                type="button"
                class="h-1.5 rounded-full transition"
                :class="idx === project.currentImageIndex ? 'w-4 bg-neon' : 'w-1.5 bg-white/35'"
                :aria-label="`Image ${idx + 1}`"
                @click.stop="setImage(project, idx)"
              />
            </div>
          </template>

          <span class="absolute top-2.5 right-2.5 rounded-md border border-neon/30 bg-navy/85 px-2.5 py-1 text-[0.7rem] font-semibold tracking-wide text-neon uppercase">
            {{ project.category }}
          </span>
        </div>

        <div class="flex flex-1 flex-col justify-between p-5">
          <div>
            <div class="mb-3 flex items-center gap-3">
              <div class="flex h-9.5 w-9.5 shrink-0 items-center justify-center rounded-[10px] bg-neon/10">
                <i :class="[project.icon, 'text-neon']"></i>
              </div>
              <h3 class="text-[1.1rem] leading-snug text-light">{{ project.title }}</h3>
            </div>
            <p class="mb-5 text-sm leading-relaxed text-slate-300">{{ project.description }}</p>
          </div>

          <div class="flex flex-wrap gap-1.5">
            <span
              v-for="tag in project.tags"
              :key="tag"
              class="rounded px-2 py-0.5 text-[0.72rem] text-slate-400 bg-navy/60"
            >
              {{ tag }}
            </span>
          </div>
        </div>
      </article>
    </div>
  </div>
</template>
