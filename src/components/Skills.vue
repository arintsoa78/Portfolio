<script setup>
import { ref } from 'vue'

// Liste des compétences regroupées par catégorie
const skillCategories = ref([
  {
    title: 'Administration Systèmes',
    icon: 'fa-solid fa-server',
    skills: [
      { name: 'Linux (Kali, Ubuntu)', level: 80 },
      { name: 'Windows Server / Active Directory', level: 70 },
      { name: 'Services (DNS Bind, DHCP, Apache/Nginx)', level: 75 },
      { name: 'Virtualisation (VirtualBox, VMware)', level: 70 }
    ]
  },
  {
    title: 'Réseaux & Protocoles',
    icon: 'fa-solid fa-network-wired',
    skills: [
      { name: 'Architecture TCP/IP, Adressage & Subnetting', level: 85 },
      { name: 'Configuration Switchs & Routeurs (Cisco/Packet Tracer)', level: 75 },
      { name: 'Protocoles (VLAN, RIP, OSPF)', level: 70 },
      { name: 'Analyse de trafic (Wireshark)', level: 80 }
    ]
  },
  {
    title: 'Sécurité & Automation',
    icon: 'fa-solid fa-shield-halved',
    skills: [
      { name: 'Firewalling (IPTables, UFW)', level: 70 },
      { name: 'Scripting Bash / Shell', level: 75 },
      { name: 'Bases en Python', level: 60 }
    ]
  }
])

// Outils et technologies secondaires (Badges)
const tools = ref([
  { name: 'Cisco Packet Tracer', icon: 'fa-solid fa-diagram-project' },
  { name: 'Wireshark', icon: 'fa-solid fa-eye' },
  { name: 'Git & GitHub', icon: 'fa-brands fa-github' },
  { name: 'VS Code', icon: 'fa-solid fa-code' },
])
</script>

<template>
  <section class="skills-section" id="skills">
    <!-- En-tête de section -->
    <div class="section-title">
      <h2>Mes <span>Compétences</span></h2>
      <div class="underline"></div>
      <p class="subtitle">
        Aperçu technique des domaines que j'étudie et pratique au quotidien en administration systèmes et réseaux.
      </p>
    </div>

    <!-- Grille des compétences clés -->
    <div class="skills-grid">
      <div 
        v-for="(category, index) in skillCategories" 
        :key="index" 
        class="skill-card"
      >
        <div class="card-header">
          <div class="icon-box">
            <i :class="category.icon"></i>
          </div>
          <h3>{{ category.title }}</h3>
        </div>

        <div class="skill-list">
          <div 
            v-for="(skill, sIndex) in category.skills" 
            :key="sIndex" 
            class="skill-item"
          >
            <div class="skill-info">
              <span class="skill-name">{{ skill.name }}</span>
              <span class="skill-percentage">{{ skill.level }}%</span>
            </div>
            <div class="progress-bar">
              <div 
                class="progress-fill" 
                :style="{ width: skill.level + '%' }"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Section Outils & Logiciels -->
    <div class="tools-wrapper">
      <h3>Environnement & Outils</h3>
      <div class="tools-grid">
        <div v-for="(tool, tIndex) in tools" :key="tIndex" class="tool-badge">
          <i :class="tool.icon"></i>
          <span>{{ tool.name }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills-section {
  padding: 60px 0;
}

/* Titre de section */
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

.subtitle {
  color: #94a3b8;
  margin-top: 15px;
  font-size: 1.05rem;
  max-width: 650px;
  margin-left: auto;
  margin-right: auto;
}

/* Grille principale des cartes */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 30px;
  margin-bottom: 50px;
}

.skill-card {
  background-color: rgba(30, 41, 59, 0.7);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 16px;
  padding: 30px;
  transition: transform 0.3s ease, border-color 0.3s ease;
}

.skill-card:hover {
  transform: translateY(-5px);
  border-color: rgba(56, 189, 248, 0.3);
}

.card-header {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 25px;
}

.icon-box {
  width: 45px;
  height: 45px;
  background-color: rgba(56, 189, 248, 0.1);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.icon-box i {
  color: #38bdf8;
  font-size: 1.3rem;
}

.card-header h3 {
  font-size: 1.25rem;
  color: #f8fafc;
  font-weight: 600;
}

/* Barres de progression */
.skill-list {
  display: flex;
  flex-direction: column;
  gap: 18px;
}

.skill-info {
  display: flex;
  justify-content: space-between;
  margin-bottom: 6px;
  font-size: 0.9rem;
}

.skill-name {
  color: #cbd5e1;
  font-weight: 500;
}

.skill-percentage {
  color: #38bdf8;
  font-weight: 600;
}

.progress-bar {
  width: 100%;
  height: 8px;
  background-color: rgba(15, 23, 42, 0.6);
  border-radius: 10px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, #2563eb, #38bdf8);
  border-radius: 10px;
  transition: width 1s ease-in-out;
}

/* Section Outils & Badges */
.tools-wrapper {
  background-color: rgba(30, 41, 59, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  padding: 30px;
  text-align: center;
}

.tools-wrapper h3 {
  color: #f8fafc;
  font-size: 1.3rem;
  margin-bottom: 25px;
}

.tools-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 15px;
}

.tool-badge {
  display: flex;
  align-items: center;
  gap: 10px;
  background-color: rgba(15, 23, 42, 0.7);
  border: 1px solid rgba(255, 255, 255, 0.08);
  padding: 10px 18px;
  border-radius: 12px;
  color: #cbd5e1;
  font-size: 0.9rem;
  font-weight: 500;
  transition: all 0.3s ease;
}

.tool-badge i {
  color: #38bdf8;
  font-size: 1.1rem;
}

.tool-badge:hover {
  border-color: #38bdf8;
  color: #f8fafc;
  transform: translateY(-3px);
}

/* Responsive */
@media (max-width: 768px) {
  .skills-grid {
    grid-template-columns: 1fr;
  }
}
</style>