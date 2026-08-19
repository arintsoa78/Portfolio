<script setup>
import { ref } from 'vue'

const formData = ref({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const isSubmitting = ref(false)
const showSuccessMessage = ref(false)
const showErrorMessage = ref(false)

const handleSubmit = async () => {
  isSubmitting.value = true
  showSuccessMessage.value = false
  showErrorMessage.value = false

  try {
    const response = await fetch('https://formspree.io/f/xzepvqzo', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Accept: 'application/json'
      },
      body: JSON.stringify({
        name: formData.value.name,
        email: formData.value.email,
        subject: formData.value.subject,
        message: formData.value.message
      })
    })

    if (response.ok) {
      showSuccessMessage.value = true
      formData.value = { name: '', email: '', subject: '', message: '' }
      setTimeout(() => {
        showSuccessMessage.value = false
      }, 6000)
    } else {
      showErrorMessage.value = true
    }
  } catch {
    showErrorMessage.value = true
  } finally {
    isSubmitting.value = false
  }
}

const contactInfo = [
  {
    icon: 'fa-solid fa-envelope',
    title: 'Email',
    value: 'anaharintsoa@gmail.com',
    href: 'mailto:anaharintsoa@gmail.com'
  },
  {
    icon: 'fa-solid fa-phone',
    title: 'Téléphone',
    value: '+261 38 74 084 05',
    href: 'tel:+261387408405'
  },
  {
    icon: 'fa-solid fa-mobile-screen',
    title: 'Téléphone (2)',
    value: '+261 33 40 183 14',
    href: 'tel:+261334018314'
  },
  {
    icon: 'fa-solid fa-location-dot',
    title: 'Localisation',
    value: 'Antananarivo / Fianarantsoa, Madagascar',
    href: null
  }
]

const socialLinks = [
  { icon: 'fa-brands fa-github', href: 'https://github.com/arintsoa78', label: 'GitHub' }
]
</script>

<template>
  <div class="py-6">
    <div class="mb-12 text-center">
      <h2 class="text-[2.2rem] font-bold text-light">
        Me <span class="text-neon">Contacter</span>
      </h2>
      <div class="mx-auto mt-2.5 h-1 w-15 rounded-sm bg-linear-to-r from-neon to-accent" />
      <p class="mx-auto mt-4 max-w-xl text-[1.05rem] text-slate-400">
        Vous cherchez une stagiaire motivée en Administration Systèmes &amp; Réseaux ? N'hésitez pas à me laisser un message !
      </p>
    </div>

    <div class="grid items-start gap-12 lg:grid-cols-[1fr_1.2fr]">
      <div>
        <h3 class="mb-4 text-[1.6rem] text-light">Restons en contact</h3>
        <p class="mb-8 leading-relaxed text-slate-300">
          Disponible pour un entretien ou des opportunités de stage. Je vous répondrai dans les meilleurs délais.
        </p>

        <div class="mb-10 flex flex-col gap-5">
          <div
            v-for="info in contactInfo"
            :key="info.title"
            class="flex items-center gap-5 rounded-xl border border-white/5 bg-card/60 px-5 py-4"
          >
            <div class="flex h-12 w-12 items-center justify-center rounded-[10px] bg-neon/10">
              <i :class="[info.icon, 'text-xl text-neon']"></i>
            </div>
            <div class="flex flex-col">
              <span class="text-xs tracking-wide text-slate-400 uppercase">{{ info.title }}</span>
              <a
                v-if="info.href"
                :href="info.href"
                class="font-medium text-light no-underline transition hover:text-neon"
              >
                {{ info.value }}
              </a>
              <span v-else class="font-medium text-light">{{ info.value }}</span>
            </div>
          </div>
        </div>

        <div>
          <h4 class="mb-4 text-[1.1rem] text-light">Suivez-moi</h4>
          <div class="flex gap-4">
            <a
              v-for="social in socialLinks"
              :key="social.label"
              :href="social.href"
              target="_blank"
              rel="noopener noreferrer"
              :aria-label="social.label"
              class="flex h-11 w-11 items-center justify-center rounded-xl border border-white/8 bg-card/80 text-light no-underline transition hover:-translate-y-0.5 hover:bg-neon hover:text-navy"
            >
              <i :class="social.icon"></i>
            </a>
          </div>
        </div>
      </div>

      <div class="rounded-2xl border border-white/8 bg-card/70 p-6 shadow-[0_15px_35px_rgb(0_0_0_/_0.3)] backdrop-blur-md sm:p-9">
        <form class="flex flex-col" @submit.prevent="handleSubmit">
          <div class="mb-5 flex flex-col gap-2">
            <label for="name" class="text-sm font-medium text-slate-300">Nom</label>
            <input
              id="name"
              v-model="formData.name"
              type="text"
              name="name"
              placeholder="Votre nom"
              required
              class="w-full rounded-[10px] border border-white/10 bg-navy/60 px-4 py-3 text-light outline-none transition focus:border-neon focus:shadow-[0_0_0_3px_rgb(56_189_248_/_0.15)]"
            />
          </div>

          <div class="mb-5 flex flex-col gap-2">
            <label for="email" class="text-sm font-medium text-slate-300">Email</label>
            <input
              id="email"
              v-model="formData.email"
              type="email"
              name="email"
              placeholder="votre.email@example.com"
              required
              class="w-full rounded-[10px] border border-white/10 bg-navy/60 px-4 py-3 text-light outline-none transition focus:border-neon focus:shadow-[0_0_0_3px_rgb(56_189_248_/_0.15)]"
            />
          </div>

          <div class="mb-5 flex flex-col gap-2">
            <label for="subject" class="text-sm font-medium text-slate-300">Objet</label>
            <input
              id="subject"
              v-model="formData.subject"
              type="text"
              name="subject"
              placeholder="Objet de votre message"
              required
              class="w-full rounded-[10px] border border-white/10 bg-navy/60 px-4 py-3 text-light outline-none transition focus:border-neon focus:shadow-[0_0_0_3px_rgb(56_189_248_/_0.15)]"
            />
          </div>

          <div class="mb-5 flex flex-col gap-2">
            <label for="message" class="text-sm font-medium text-slate-300">Message</label>
            <textarea
              id="message"
              v-model="formData.message"
              name="message"
              rows="5"
              placeholder="Votre message ici..."
              required
              class="w-full rounded-[10px] border border-white/10 bg-navy/60 px-4 py-3 text-light outline-none transition focus:border-neon focus:shadow-[0_0_0_3px_rgb(56_189_248_/_0.15)]"
            />
          </div>

          <button
            type="submit"
            class="flex w-full items-center justify-center gap-2.5 rounded-[10px] bg-linear-to-br from-blue-600 to-blue-700 px-4 py-3.5 font-semibold text-white transition hover:-translate-y-0.5 hover:shadow-[0_10px_25px_-5px_rgb(37_99_235_/_0.5)] disabled:cursor-not-allowed disabled:opacity-70"
            :disabled="isSubmitting"
          >
            <span v-if="!isSubmitting">
              <i class="fa-solid fa-paper-plane"></i> Envoyer le message
            </span>
            <span v-else>
              <i class="fa-solid fa-spinner fa-spin"></i> Envoi en cours...
            </span>
          </button>

          <Transition
            enter-active-class="transition-opacity duration-500"
            leave-active-class="transition-opacity duration-500"
            enter-from-class="opacity-0"
            leave-to-class="opacity-0"
          >
            <div
              v-if="showSuccessMessage"
              class="mt-5 flex items-center gap-2.5 rounded-[10px] border border-green-500/40 bg-green-500/15 px-4 py-3 text-sm text-green-400"
            >
              <i class="fa-solid fa-circle-check"></i>
              <span>Merci ! Votre message a été envoyé avec succès.</span>
            </div>
          </Transition>

          <Transition
            enter-active-class="transition-opacity duration-500"
            leave-active-class="transition-opacity duration-500"
            enter-from-class="opacity-0"
            leave-to-class="opacity-0"
          >
            <div
              v-if="showErrorMessage"
              class="mt-5 flex items-center gap-2.5 rounded-[10px] border border-red-500/40 bg-red-500/15 px-4 py-3 text-sm text-red-400"
            >
              <i class="fa-solid fa-triangle-exclamation"></i>
              <span>Une erreur s'est produite lors de l'envoi. Veuillez réessayer.</span>
            </div>
          </Transition>
        </form>
      </div>
    </div>
  </div>
</template>
