<script setup>
const qualities = [
  'Esprit d\'analyse',
  'Rigueur & Autonomie',
  'Sens de l\'organisation',
  'Travail en équipe',
  'Curiosité & Apprentissage rapide'
]

const languages = [
  { name: 'Malagasy', level: 'Langue maternelle' },
  { name: 'Français', level: 'Courant' },
  { name: 'Anglais', level: 'Intermédiaire' }
]
</script>

<template>
  <div class="py-6">
    <div class="mb-12 text-center">
      <h2 class="text-[2.2rem] font-bold text-light">
        À propos de <span class="text-neon">Moi</span>
      </h2>
      <div class="mx-auto mt-2.5 h-1 w-15 rounded-sm bg-linear-to-r from-neon to-accent" />
    </div>

    <div class="grid gap-8 lg:grid-cols-[1.2fr_1fr]">
      <div class="rounded-2xl border border-white/8 bg-card/70 p-8 backdrop-blur-md">
        <h3 class="mb-1 text-2xl text-light">HARIMANANTSOA Tsiresy Espérencia</h3>
        <p class="mb-5 font-medium text-neon">
          Étudiante en L2 Informatique (ENI) | Stagiaire en Administration Système &amp; Réseaux
        </p>
        <p class="mb-4 leading-relaxed text-slate-300">
          Étudiante en deuxième année de Licence en Informatique à l'École Nationale d'Informatique (ENI), passionnée par les systèmes et réseaux, je recherche un stage en Administration Systèmes et Réseaux afin de développer mes compétences et contribuer à des projets concrets.
        </p>

        <div class="mt-8">
          <h4 class="mb-4 text-light">Mes Qualités</h4>
          <div class="flex flex-wrap gap-2.5">
            <span
              v-for="quality in qualities"
              :key="quality"
              class="rounded-full border border-neon/20 bg-neon/10 px-3.5 py-1.5 text-sm font-medium text-neon"
            >
              <i class="fa-solid fa-check"></i> {{ quality }}
            </span>
          </div>
        </div>
      </div>

      <div class="flex flex-col gap-5">
        <div class="rounded-2xl border border-white/8 bg-card/70 p-8 backdrop-blur-md">
          <h3 class="mb-5 flex items-center gap-2.5 text-xl text-light">
            <i class="fa-solid fa-graduation-cap text-neon"></i> Formations
          </h3>
          <div class="flex flex-col gap-4 border-l-2 border-neon/30 pl-4">
            <div>
              <span class="text-xs font-semibold text-neon">2025 - 2026</span>
              <p class="text-sm font-medium text-light">Licence 2 - Informatique Général</p>
              <p class="text-sm text-slate-400">École Nationale d'Informatique (ENI)</p>
            </div>
            <div>
              <span class="text-xs font-semibold text-neon">2024 - 2025</span>
              <p class="text-sm font-medium text-light">Licence 1 - Informatique Général</p>
              <p class="text-sm text-slate-400">École Nationale d'Informatique (ENI)</p>
            </div>
            <div>
              <span class="text-xs font-semibold text-neon">2023 - 2024</span>
              <p class="text-sm font-medium text-light">Baccalauréat Série D</p>
              <p class="text-sm text-slate-400">Lycée Saint François Xavier Fianarantsoa</p>
            </div>
          </div>
        </div>

        <div class="rounded-2xl border border-white/8 bg-card/70 p-8 backdrop-blur-md">
          <h3 class="mb-5 flex items-center gap-2.5 text-xl text-light">
            <i class="fa-solid fa-language text-neon"></i> Langues
          </h3>
          <div class="flex flex-col gap-2.5">
            <div
              v-for="lang in languages"
              :key="lang.name"
              class="flex justify-between border-b border-white/5 pb-2"
            >
              <span class="font-medium text-light">{{ lang.name }}</span>
              <span class="text-sm text-slate-400">{{ lang.level }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
