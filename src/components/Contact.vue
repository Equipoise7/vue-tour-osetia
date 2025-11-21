<script setup>
import whatsappIcon from '../assets/icons/whatsapp.svg'
import telegramIcon from '../assets/icons/telegram.svg'

const phone = '+7 (989) 741-36-34'
const phoneClean = '79897413634'
const whatsappLink = `https://wa.me/${phoneClean}`
const telegramLink = `https://t.me/transfer15reg`
</script>

<template>
  <section id="contact" class="contact">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Связаться с нами</h2>
        <p class="section-subtitle">Выберите удобный способ связи</p>
      </div>

      <div class="contact-grid">
        <!-- Телефон -->
        <div class="contact-card phone-card">
          <div class="card-icon">📞</div>
          <div class="card-content">
            <h3 class="card-title">Позвоните</h3>
            <a :href="`tel:${phoneClean}`" class="phone-number">{{ phone }}</a>
            <p class="card-description">8:00 - 22:00</p>
          </div>
        </div>

        <!-- WhatsApp -->
        <a :href="whatsappLink" target="_blank" class="contact-card messenger-card">
          <div class="card-icon">
            <img :src="whatsappIcon" alt="WhatsApp" />
          </div>
          <div class="card-content">
            <h3 class="card-title">WhatsApp</h3>
            <p class="card-description">Быстрые ответы</p>
          </div>
        </a>

        <!-- Telegram -->
        <a :href="telegramLink" target="_blank" class="contact-card messenger-card">
          <div class="card-icon">
            <img :src="telegramIcon" alt="Telegram" />
          </div>
          <div class="card-content">
            <h3 class="card-title">Telegram</h3>
            <p class="card-description">Удобный чат</p>
          </div>
        </a>

        <!-- Email -->
        <a href="mailto:Transfer15rus@yandex.ru" class="contact-card email-card">
          <div class="card-icon">✉️</div>
          <div class="card-content">
            <h3 class="card-title">Email</h3>
            <p class="card-description">Transfer15rus@yandex.ru</p>
          </div>
        </a>
      </div>

      <div class="location-bar">
        <span class="location-icon">📍</span>
        <span>г. Владикавказ, Республика Северная Осетия-Алания</span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact {
  padding: 4rem 0;
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  position: relative;
  overflow: hidden;
}

.container {
  max-width: 900px;
  margin: 0 auto;
  padding: 0 2rem;
  position: relative;
  z-index: 1;
}

.section-header {
  text-align: center;
  margin-bottom: 2.5rem;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 800;
  color: white;
  margin-bottom: 0.5rem;
}

.section-subtitle {
  font-size: 1.1rem;
  color: rgba(255, 255, 255, 0.9);
}

.contact-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.contact-card {
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(10px);
  padding: 1.5rem 1rem;
  border-radius: 15px;
  text-align: center;
  border: 2px solid rgba(255, 255, 255, 0.2);
  transition: all 0.3s ease;
  text-decoration: none;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.contact-card:hover {
  transform: translateY(-5px);
  background: rgba(255, 255, 255, 0.25);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.card-icon {
  font-size: 2.5rem;
  margin-bottom: 0.75rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-icon img {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  object-fit: cover;
}

.card-content {
  text-align: center;
}

.card-title {
  font-size: 1.1rem;
  font-weight: 700;
  color: white;
  margin-bottom: 0.5rem;
}

.phone-number {
  display: block;
  font-size: 1.1rem;
  font-weight: 700;
  color: white;
  text-decoration: none;
  margin-bottom: 0.25rem;
  transition: all 0.3s ease;
}

.phone-number:hover {
  transform: scale(1.05);
}

.card-description {
  color: rgba(255, 255, 255, 0.85);
  font-size: 0.85rem;
  line-height: 1.4;
  word-break: break-word;
}

.location-bar {
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(10px);
  padding: 1rem 1.5rem;
  border-radius: 50px;
  text-align: center;
  border: 2px solid rgba(255, 255, 255, 0.2);
  color: white;
  font-size: 0.95rem;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
}

.location-icon {
  font-size: 1.2rem;
}

@media (max-width: 768px) {
  .contact {
    padding: 3rem 0;
  }

  .section-title {
    font-size: 2rem;
  }

  .section-subtitle {
    font-size: 1rem;
  }

  .contact-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 0.75rem;
  }

  .contact-card {
    padding: 1.25rem 0.75rem;
  }

  .card-icon {
    font-size: 2rem;
    margin-bottom: 0.5rem;
  }

  .card-icon img {
    width: 32px;
    height: 32px;
  }

  .card-title {
    font-size: 1rem;
  }

  .phone-number {
    font-size: 0.95rem;
  }

  .card-description {
    font-size: 0.75rem;
  }

  .location-bar {
    padding: 0.875rem 1rem;
    font-size: 0.85rem;
  }
}

@media (max-width: 480px) {
  .contact-grid {
    grid-template-columns: 1fr;
  }
}
</style>
