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
  <section class="about-section" id="about">
    <div class="section-title">
      <h2>À propos de <span>Moi</span></h2>
      <div class="underline"></div>
    </div>

    <div class="about-grid">
      <!-- Bio & Présentation -->
      <div class="about-text-card">
        <h3>HARIMANANTSOA Tsiresy Espérencia</h3>
        <p class="subtitle">Étudiante en L2 Informatique (ENI) | Stagiaire en Administration Système & Réseaux</p>
        
        <p class="description">
          Étudiante en deuxième année de Licence en Informatique à l'École Nationale d'Informatique (ENI),  Passionnée par les systèmes et réseaux, je recherche un stage
        en Administration Systèmes et Réseaux afin de développer mes
        compétences et contribuer à des projets concrets.
        </p>
        

        <!-- Qualités sous forme de badges -->
        <div class="qualities-wrapper">
          <h4>Mes Qualités</h4>
          <div class="tags">
            <span v-for="(quality, index) in qualities" :key="index" class="quality-tag">
              <i class="fa-solid fa-check"></i> {{ quality }}
            </span>
          </div>
        </div>
      </div>

      <!-- Formations & Langues -->
      <div class="side-info">
        <!-- Paragraphe Formations -->
        <div class="info-card">
          <h3><i class="fa-solid fa-graduation-cap"></i> Formations</h3>
          <div class="timeline">
            <div class="timeline-item">
              <span class="year">2025 - 2026</span>
              <p class="degree">Licence 2 - Informatique Général</p>
              <p class="school">École Nationale d'Informatique (ENI)</p>
            </div>
            <div class="timeline-item">
              <span class="year">2024 - 2025</span>
              <p class="degree">Licence 1 - Informatique Général</p>
              <p class="school">École Nationale d'Informatique (ENI)</p>
            </div>
            <div class="timeline-item">
              <span class="year">2023 - 2024</span>
              <p class="degree">Baccalauréat Série D</p>
              <p class="school">Lycée Saint François Xavier Fianarantsoa</p>
            </div>
          </div>
        </div>

        <!-- Langues -->
        <div class="info-card">
          <h3><i class="fa-solid fa-language"></i> Langues</h3>
          <div class="languages-list">
            <div v-for="(lang, i) in languages" :key="i" class="lang-item">
              <span class="lang-name">{{ lang.name }}</span>
              <span class="lang-level">{{ lang.level }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>

  </section>
</template>

<style scoped>
.about-section {
  padding: 60px 0;
}

.section-title {
  text-align: center;
  margin-bottom: 50px;
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

.about-grid {
  display: grid;
  grid-template-columns: 1.2fr 1fr;
  gap: 30px;
  margin-bottom: 40px;
}

.about-text-card, .info-card {
  background-color: rgba(30, 41, 59, 0.7);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 16px;
  padding: 30px;
}

.about-text-card h3 {
  font-size: 1.5rem;
  color: #f8fafc;
  margin-bottom: 5px;
}

.subtitle {
  color: #38bdf8;
  font-weight: 500;
  margin-bottom: 20px;
}

.description {
  color: #cbd5e1;
  line-height: 1.7;
  margin-bottom: 15px;
}

.qualities-wrapper {
  margin-top: 30px;
}

.qualities-wrapper h4 {
  color: #f8fafc;
  margin-bottom: 15px;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.quality-tag {
  background-color: rgba(56, 189, 248, 0.1);
  color: #38bdf8;
  border: 1px solid rgba(56, 189, 248, 0.2);
  padding: 6px 14px;
  border-radius: 20px;
  font-size: 0.85rem;
  font-weight: 500;
}

/* Timeline Formations */
.side-info {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.info-card h3 {
  font-size: 1.2rem;
  color: #f8fafc;
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  gap: 10px;
}

.info-card h3 i {
  color: #38bdf8;
}

.timeline {
  display: flex;
  flex-direction: column;
  gap: 15px;
  border-left: 2px solid rgba(56, 189, 248, 0.3);
  padding-left: 15px;
}

.timeline-item {
  position: relative;
}

.year {
  font-size: 0.8rem;
  color: #38bdf8;
  font-weight: 600;
}

.degree {
  color: #f8fafc;
  font-weight: 500;
  font-size: 0.95rem;
}

.school {
  color: #94a3b8;
  font-size: 0.85rem;
}

/* Langues */
.languages-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.lang-item {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  padding-bottom: 8px;
}

.lang-name {
  color: #f8fafc;
  font-weight: 500;
}

.lang-level {
  color: #94a3b8;
  font-size: 0.85rem;
}

/* Centres d'intérêt */
.interests-wrapper {
  background-color: rgba(30, 41, 59, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  padding: 25px;
  text-align: center;
}

.interests-wrapper h3 {
  color: #f8fafc;
  margin-bottom: 20px;
}

.interests-grid {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 15px;
}

.interest-card {
  display: flex;
  align-items: center;
  gap: 10px;
  background-color: rgba(15, 23, 42, 0.6);
  padding: 10px 20px;
  border-radius: 12px;
  color: #cbd5e1;
  font-size: 0.9rem;
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.interest-card i {
  color: #38bdf8;
}

@media (max-width: 968px) {
  .about-grid {
    grid-template-columns: 1fr;
  }
}
</style>