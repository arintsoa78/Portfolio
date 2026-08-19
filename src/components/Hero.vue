<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const personalInfo = {
  name: 'HARIMANANTSOA Tsiresy Espérencia',
  subtitles: [
    'Étudiante en L2 Informatique',
    'Administratrice Systèmes & Réseaux',
    'Passionnée de Cybersécurité'
  ],
  bio: 'Actuellement en recherche d\'un stage. Je conçois, simule et sécurise des infrastructures réseaux complexes (GNS3, Cisco, Windows Server) tout en développant mes compétences sur Linux.'
}

const currentSubtitleIndex = ref(0)
const currentText = ref('')
const isDeleting = ref(false)
let timer = null

const typeEffect = () => {
  const fullText = personalInfo.subtitles[currentSubtitleIndex.value]

  if (isDeleting.value) {
    currentText.value = fullText.substring(0, currentText.value.length - 1)
  } else {
    currentText.value = fullText.substring(0, currentText.value.length + 1)
  }

  let typeSpeed = isDeleting.value ? 50 : 100

  if (!isDeleting.value && currentText.value === fullText) {
    typeSpeed = 2000
    isDeleting.value = true
  } else if (isDeleting.value && currentText.value === '') {
    isDeleting.value = false
    currentSubtitleIndex.value = (currentSubtitleIndex.value + 1) % personalInfo.subtitles.length
    typeSpeed = 500
  }

  timer = setTimeout(typeEffect, typeSpeed)
}

onMounted(() => {
  typeEffect()
})

onUnmounted(() => {
  if (timer) clearTimeout(timer)
})

const stats = [
  { icon: 'fa-solid fa-graduation-cap', label: 'Niveau', value: 'Licence 2' },
  { icon: 'fa-solid fa-network-wired', label: 'Spécialité', value: 'Systèmes & Réseaux' },
  { icon: 'fa-solid fa-briefcase', label: 'Objectif', value: 'Stage Pro' }
]

const socialLinks = [
  { icon: 'fa-brands fa-github', href: 'https://github.com/arintsoa78', label: 'GitHub' }
]
</script>

<template>
  <div class="relative flex min-h-[85vh] items-center overflow-hidden py-10">
    <div class="animate-glow pointer-events-none absolute top-[10%] -left-[5%] z-0 h-[350px] w-[350px] rounded-full bg-neon opacity-15 blur-[120px]" />
    <div class="animate-glow pointer-events-none absolute right-[-5%] bottom-[10%] z-0 h-[400px] w-[400px] rounded-full bg-accent opacity-15 blur-[120px]" />

    <div class="relative z-1 grid w-full items-center gap-12 lg:grid-cols-[1.2fr_0.8fr]">
      <div class="flex flex-col items-center text-center lg:items-start lg:text-left">
        <div class="mb-6 inline-flex items-center gap-2.5 rounded-full border border-green-500/30 bg-green-500/10 px-4 py-1.5 text-sm font-medium text-green-400">
          <span class="animate-pulse-dot h-2 w-2 rounded-full bg-green-500" />
          <span>Disponible pour un stage</span>
        </div>

        <h1 class="mb-4 text-3xl leading-tight font-extrabold text-light sm:text-4xl lg:text-[2.8rem]">
          Bonjour, je suis <br />
          <span class="bg-linear-to-br from-neon to-accent bg-clip-text text-transparent">
            {{ personalInfo.name }}
          </span>
        </h1>

        <div class="mb-5 flex min-h-10 items-center text-xl font-semibold text-slate-300">
          <span class="text-neon">{{ currentText }}</span>
          <span class="animate-blink ml-0.5 text-neon">|</span>
        </div>

        <p class="mb-8 max-w-xl text-[1.05rem] leading-relaxed text-slate-400">
          {{ personalInfo.bio }}
        </p>

        <div class="mb-9 flex flex-wrap justify-center gap-5 lg:justify-start">
          <div
            v-for="stat in stats"
            :key="stat.label"
            class="flex items-center gap-4 rounded-xl border border-white/5 bg-card/60 px-4.5 py-3 backdrop-blur-md"
          >
            <i :class="[stat.icon, 'text-xl text-neon']"></i>
            <div>
              <span class="block text-sm font-bold text-light">{{ stat.value }}</span>
              <span class="text-xs text-slate-400">{{ stat.label }}</span>
            </div>
          </div>
        </div>

        <div class="mb-8 flex flex-wrap justify-center gap-3.5 lg:justify-start">
          <a
            href="#projects"
            class="inline-flex items-center gap-2.5 rounded-xl bg-linear-to-br from-blue-600 to-blue-700 px-7 py-3.5 text-sm font-semibold text-white no-underline shadow-[0_10px_25px_-5px_rgb(37_99_235_/_0.4)] transition hover:-translate-y-0.5 hover:shadow-[0_15px_30px_-5px_rgb(37_99_235_/_0.6)]"
          >
            <span>Découvrir mes projets</span>
            <i class="fa-solid fa-arrow-right"></i>
          </a>
          <a
            href="#contact"
            class="inline-flex items-center gap-2.5 rounded-xl border border-white/10 bg-card/80 px-7 py-3.5 text-sm font-semibold text-light no-underline transition hover:-translate-y-0.5 hover:border-neon hover:text-neon"
          >
            <span>Me Contacter</span>
            <i class="fa-solid fa-paper-plane"></i>
          </a>
          <a
            href="/CV_Esperencia.pdf"
            download="CV_Esperencia.pdf"
            class="inline-flex items-center gap-2.5 rounded-xl bg-linear-to-br from-blue-600 to-blue-700 px-7 py-3.5 text-sm font-semibold text-white no-underline shadow-[0_10px_25px_-5px_rgb(37_99_235_/_0.4)] transition hover:-translate-y-0.5"
          >
            <span>Télécharger CV</span>
            <i class="fa-solid fa-download"></i>
          </a>
        </div>

        <div class="flex justify-center gap-3 lg:justify-start">
          <a
            v-for="social in socialLinks"
            :key="social.label"
            :href="social.href"
            target="_blank"
            rel="noopener noreferrer"
            :aria-label="social.label"
            class="flex h-[42px] w-[42px] items-center justify-center rounded-xl border border-white/8 bg-card/80 text-light no-underline transition hover:-translate-y-0.5 hover:bg-neon hover:text-navy"
          >
            <i :class="social.icon"></i>
          </a>
        </div>
      </div>

      <div class="flex items-center justify-center">
        <div class="animate-orbit relative flex h-[250px] w-[250px] items-center justify-center rounded-full border-2 border-dashed border-neon/20 lg:h-[300px] lg:w-[300px]">
          <div class="animate-counter-orbit flex h-[90px] w-[90px] items-center justify-center rounded-full border-2 border-neon bg-linear-to-br from-card to-navy shadow-[0_0_30px_rgb(56_189_248_/_0.3)]">
            <i class="fa-solid fa-server text-[2.2rem] text-neon"></i>
          </div>

          <div class="animate-counter-orbit absolute -top-4 flex items-center gap-2 rounded-full border border-neon/30 bg-card/90 px-3.5 py-2 text-sm font-medium text-light shadow-lg">
            <i class="fa-solid fa-network-wired text-neon"></i>
            <span>GNS3</span>
          </div>
          <div class="animate-counter-orbit absolute -right-5 flex items-center gap-2 rounded-full border border-neon/30 bg-card/90 px-3.5 py-2 text-sm font-medium text-light shadow-lg">
            <i class="fa-brands fa-linux text-neon"></i>
            <span>Linux</span>
          </div>
          <div class="animate-counter-orbit absolute -bottom-4 flex items-center gap-2 rounded-full border border-neon/30 bg-card/90 px-3.5 py-2 text-sm font-medium text-light shadow-lg">
            <i class="fa-brands fa-windows text-neon"></i>
            <span>Windows</span>
          </div>
          <div class="animate-counter-orbit absolute -left-5 flex items-center gap-2 rounded-full border border-neon/30 bg-card/90 px-3.5 py-2 text-sm font-medium text-light shadow-lg">
            <i class="fa-solid fa-shield-halved text-neon"></i>
            <span>Cisco</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
