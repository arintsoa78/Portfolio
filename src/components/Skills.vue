<script setup>
import { ref } from 'vue'

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

const tools = ref([
  { name: 'GNS3', icon: 'fa-solid fa-network-wired' },
  { name: 'Cisco Packet Tracer', icon: 'fa-solid fa-diagram-project' },
  { name: 'Wireshark', icon: 'fa-solid fa-eye' },
  { name: 'Git & GitHub', icon: 'fa-brands fa-github' },
  { name: 'VS Code', icon: 'fa-solid fa-code' }
])
</script>

<template>
  <div class="py-6">
    <div class="mb-12 text-center">
      <h2 class="text-[2.2rem] font-bold text-light">
        Mes <span class="text-neon">Compétences</span>
      </h2>
      <div class="mx-auto mt-2.5 h-1 w-15 rounded-sm bg-linear-to-r from-neon to-accent" />
      <p class="mx-auto mt-4 max-w-xl text-[1.05rem] text-slate-400">
        Aperçu technique des domaines que j'étudie et pratique au quotidien en administration systèmes et réseaux.
      </p>
    </div>

    <div class="mb-12 grid grid-cols-1 gap-8 md:grid-cols-2 xl:grid-cols-3">
      <div
        v-for="category in skillCategories"
        :key="category.title"
        class="rounded-2xl border border-white/8 bg-card/70 p-8 backdrop-blur-md transition hover:-translate-y-1 hover:border-neon/30"
      >
        <div class="mb-6 flex items-center gap-4">
          <div class="flex h-11 w-11 items-center justify-center rounded-xl bg-neon/10">
            <i :class="[category.icon, 'text-xl text-neon']"></i>
          </div>
          <h3 class="text-xl font-semibold text-light">{{ category.title }}</h3>
        </div>

        <div class="flex flex-col gap-4.5">
          <div v-for="skill in category.skills" :key="skill.name">
            <div class="mb-1.5 flex justify-between text-sm">
              <span class="font-medium text-slate-300">{{ skill.name }}</span>
              <span class="font-semibold text-neon">{{ skill.level }}%</span>
            </div>
            <div class="h-2 overflow-hidden rounded-[10px] bg-navy/60">
              <div
                class="h-full rounded-[10px] bg-linear-to-r from-blue-600 to-neon"
                :style="{ width: skill.level + '%' }"
              />
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="rounded-2xl border border-white/5 bg-card/40 p-8 text-center">
      <h3 class="mb-6 text-xl text-light">Environnement &amp; Outils</h3>
      <div class="flex flex-wrap justify-center gap-4">
        <div
          v-for="tool in tools"
          :key="tool.name"
          class="flex items-center gap-2.5 rounded-xl border border-white/8 bg-navy/70 px-4.5 py-2.5 text-sm font-medium text-slate-300 transition hover:-translate-y-0.5 hover:border-neon hover:text-light"
        >
          <i :class="[tool.icon, 'text-neon']"></i>
          <span>{{ tool.name }}</span>
        </div>
      </div>
    </div>
  </div>
</template>
