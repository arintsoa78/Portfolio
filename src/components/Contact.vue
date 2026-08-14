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
        'Accept': 'application/json'
      },
      body: JSON.stringify(formData.value)
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
  } catch (error) {
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
    value: '+261 33 40 183 14',
    href: 'tel:+261334018314'
  },
  {
    icon: 'fa-solid fa-location-dot',
    title: 'Localisation',
    value: 'Antananarivo',
    href: null
  }
]

const socialLinks = [
  { icon: 'fa-brands fa-linkedin-in', href: 'https://linkedin.com', label: 'LinkedIn' },
  { icon: 'fa-brands fa-github', href: 'https://github.com/arintsoa78', label: 'GitHub' }
]
</script>

<template>
  <section class="contact-section" id="contact">
    <!-- En-tête de section -->
    <div class="section-title">
      <h2>Me <span>Contacter</span></h2>
      <div class="underline"></div>
      <p class="subtitle">
        Vous cherchez une stagiaire motivée en Administration Systèmes & Réseaux ? N'hésitez pas à me laisser un message !
      </p>
    </div>

    <div class="contact-grid">
      <!-- Colonne Informations de contact -->
      <div class="contact-info-wrapper">
        <h3>Restons en contact</h3>
        <p class="info-desc">
          Disponible pour un entretien ou des opportunités de stage. Je vous répondrai dans les meilleurs délais.
        </p>

        <div class="info-cards">
          <div v-for="(info, index) in contactInfo" :key="index" class="info-card">
            <div class="icon-box">
              <i :class="info.icon"></i>
            </div>
            <div class="info-details">
              <span class="title">{{ info.title }}</span>
              <a v-if="info.href" :href="info.href" class="value link">{{ info.value }}</a>
              <span v-else class="value">{{ info.value }}</span>
            </div>
          </div>
        </div>

        <!-- Réseaux sociaux -->
        <div class="socials">
          <h4>Suivez-moi</h4>
          <div class="social-icons">
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
      </div>

      <!-- Colonne Formulaire de contact -->
      <div class="contact-form-wrapper">
        <form @submit.prevent="handleSubmit" class="contact-form">
          <div class="form-group">
            <label for="name">Nom complet</label>
            <input 
              type="text" 
              id="name" 
              name="name"
              v-model="formData.name" 
              placeholder="Votre nom" 
              required 
            />
          </div>

          <div class="form-group">
            <label for="email">Adresse Email</label>
            <input 
              type="email" 
              id="email" 
              name="email"
              v-model="formData.email" 
              placeholder="votre.email@example.com" 
              required 
            />
          </div>

          <div class="form-group">
            <label for="subject">Sujet</label>
            <input 
              type="text" 
              id="subject" 
              name="subject"
              v-model="formData.subject" 
              placeholder="Objet de votre message" 
              required 
            />
          </div>

          <div class="form-group">
            <label for="message">Message</label>
            <textarea 
              id="message" 
              name="message"
              v-model="formData.message" 
              rows="5" 
              placeholder="Votre message ici..." 
              required
            ></textarea>
          </div>

          <button type="submit" class="submit-btn" :disabled="isSubmitting">
            <span v-if="!isSubmitting">
              <i class="fa-solid fa-paper-plane"></i> Envoyer le message
            </span>
            <span v-else>
              <i class="fa-solid fa-spinner fa-spin"></i> Envoi en cours...
            </span>
          </button>

          <!-- Notifications -->
          <transition name="fade">
            <div v-if="showSuccessMessage" class="success-alert">
              <i class="fa-solid fa-circle-check"></i>
              <span>Merci ! Votre message a été envoyé avec succès.</span>
            </div>
          </transition>

          <transition name="fade">
            <div v-if="showErrorMessage" class="error-alert">
              <i class="fa-solid fa-triangle-exclamation"></i>
              <span>Une erreur s'est produite lors de l'envoi. Veuillez réespayer.</span>
            </div>
          </transition>
        </form>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact-section {
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
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

/* Grille principale */
.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: 50px;
  align-items: start;
}

/* Colonne Infos */
.contact-info-wrapper h3 {
  font-size: 1.6rem;
  color: #f8fafc;
  margin-bottom: 15px;
}

.info-desc {
  color: #cbd5e1;
  line-height: 1.7;
  margin-bottom: 30px;
}

.info-cards {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin-bottom: 40px;
}

.info-card {
  display: flex;
  align-items: center;
  gap: 20px;
  background-color: rgba(30, 41, 59, 0.6);
  padding: 16px 20px;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.icon-box {
  width: 48px;
  height: 48px;
  background-color: rgba(56, 189, 248, 0.1);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.icon-box i {
  color: #38bdf8;
  font-size: 1.2rem;
}

.info-details {
  display: flex;
  flex-direction: column;
}

.info-details .title {
  font-size: 0.8rem;
  color: #94a3b8;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.info-details .value {
  color: #f8fafc;
  font-weight: 500;
  font-size: 1rem;
}

.info-details .link {
  text-decoration: none;
  transition: color 0.3s;
}

.info-details .link:hover {
  color: #38bdf8;
}

/* Réseaux sociaux */
.socials h4 {
  color: #f8fafc;
  font-size: 1.1rem;
  margin-bottom: 15px;
}

.social-icons {
  display: flex;
  gap: 15px;
}

.social-btn {
  width: 44px;
  height: 44px;
  border-radius: 10px;
  background-color: rgba(30, 41, 59, 0.8);
  border: 1px solid rgba(255, 255, 255, 0.08);
  color: #f8fafc;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.1rem;
  text-decoration: none;
  transition: all 0.3s ease;
}

.social-btn:hover {
  background-color: #38bdf8;
  color: #0f172a;
  transform: translateY(-3px);
}

/* Formulaire */
.contact-form-wrapper {
  background-color: rgba(30, 41, 59, 0.7);
  backdrop-filter: blur(10px);
  padding: 35px;
  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 20px;
}

.form-group label {
  color: #cbd5e1;
  font-size: 0.9rem;
  font-weight: 500;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 12px 16px;
  background-color: rgba(15, 23, 42, 0.6);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  color: #f8fafc;
  font-size: 0.95rem;
  outline: none;
  transition: border-color 0.3s, box-shadow 0.3s;
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: #38bdf8;
  box-shadow: 0 0 0 3px rgba(56, 189, 248, 0.15);
}

.submit-btn {
  width: 100%;
  padding: 14px;
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: #ffffff;
  border: none;
  border-radius: 10px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px -5px rgba(37, 99, 235, 0.5);
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

/* Alertes */
.success-alert {
  margin-top: 20px;
  padding: 12px 16px;
  background-color: rgba(34, 197, 94, 0.15);
  border: 1px solid rgba(34, 197, 94, 0.4);
  color: #4ade80;
  border-radius: 10px;
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 0.9rem;
}

.error-alert {
  margin-top: 20px;
  padding: 12px 16px;
  background-color: rgba(239, 68, 68, 0.15);
  border: 1px solid rgba(239, 68, 68, 0.4);
  color: #f87171;
  border-radius: 10px;
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 0.9rem;
}

/* Transition Vue */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* Responsive */
@media (max-width: 968px) {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 40px;
  }

  .contact-form-wrapper {
    padding: 25px;
  }
}
</style>