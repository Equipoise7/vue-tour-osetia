<script setup>
const phone = '+7 (989) 741-36-34'
const phoneClean = '79897413634'
const whatsappLink = `https://wa.me/${phoneClean}`
const telegramLink = `https://t.me/${phoneClean}`
</script>

<template>
  <section id="contact" class="contact">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Связаться с нами</h2>
        <p class="section-subtitle">Выберите удобный способ связи</p>
      </div>

      <div class="contact-content">
        <div class="contact-info">
          <div class="info-card">
            <div class="card-icon">📞</div>
            <h3 class="card-title">Позвоните нам</h3>
            <a :href="`tel:${phoneClean}`" class="phone-number">{{ phone }}</a>
            <p class="card-description">Ежедневно с 8:00 до 22:00</p>
          </div>

          <div class="contact-methods">
            <a :href="whatsappLink" target="_blank" class="method-btn whatsapp">
              <div class="method-icon">💬</div>
              <div class="method-content">
                <div class="method-name">WhatsApp</div>
                <div class="method-description">Быстрые ответы</div>
              </div>
            </a>

            <a :href="telegramLink" target="_blank" class="method-btn telegram">
              <div class="method-icon">✈️</div>
              <div class="method-content">
                <div class="method-name">Telegram</div>
                <div class="method-description">Удобный чат</div>
              </div>
            </a>
          </div>

          <div class="info-details">
            <div class="detail-item">
              <span class="detail-icon">📍</span>
              <div>
                <strong>Адрес:</strong><br>
                г. Владикавказ, Республика Северная Осетия-Алания
              </div>
            </div>
            <div class="detail-item">
              <span class="detail-icon">✉️</span>
              <div>
                <strong>Email:</strong><br>
                Transfer15rus@yandex.ru
              </div>
            </div>
          </div>
        </div>

        <div class="contact-actions">
          <div class="actions-card">
            <div class="call-large">
              <a :href="`tel:${phoneClean}`" class="call-btn">{{ phone }}</a>
              <p class="call-note">Звоните или пишите в мессенджеры — отвечаем быстро</p>
            </div>

            <div class="actions-methods">
              <a :href="whatsappLink" target="_blank" class="action-btn whatsapp">WhatsApp</a>
              <a :href="telegramLink" target="_blank" class="action-btn telegram">Telegram</a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="decorative-bg">
      <div class="mountain mountain-1"></div>
      <div class="mountain mountain-2"></div>
      <div class="mountain mountain-3"></div>
    </div>
  </section>
</template>

<style scoped>
.contact {
  padding: 6rem 0;
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  position: relative;
  overflow: hidden;
}

.decorative-bg {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 200px;
  pointer-events: none;
}

.mountain {
  position: absolute;
  bottom: 0;
  width: 0;
  height: 0;
  border-left: 150px solid transparent;
  border-right: 150px solid transparent;
  opacity: 0.1;
}

.mountain-1 {
  left: 10%;
  border-bottom: 200px solid white;
}

.mountain-2 {
  left: 40%;
  border-bottom: 150px solid white;
}

.mountain-3 {
  right: 10%;
  border-bottom: 180px solid white;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  position: relative;
  z-index: 1;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-size: 3rem;
  font-weight: 800;
  color: white;
  margin-bottom: 1rem;
}

.section-subtitle {
  font-size: 1.25rem;
  color: rgba(255, 255, 255, 0.9);
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 420px;
  gap: 3rem;
  align-items: start;
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.info-card {
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(10px);
  padding: 2.5rem;
  border-radius: 20px;
  text-align: center;
  border: 2px solid rgba(255, 255, 255, 0.2);
}

.card-icon {
  font-size: 4rem;
  margin-bottom: 1rem;
}

.card-title {
  font-size: 1.5rem;
  font-weight: 700;
  color: white;
  margin-bottom: 1rem;
}

.phone-number {
  display: block;
  font-size: 2rem;
  font-weight: 800;
  color: white;
  text-decoration: none;
  margin-bottom: 0.5rem;
  transition: all 0.3s ease;
}

.phone-number:hover {
  transform: scale(1.05);
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}

.card-description {
  color: rgba(255, 255, 255, 0.8);
  font-size: 1rem;
}

.contact-methods {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.method-btn {
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(10px);
  padding: 1.5rem;
  border-radius: 15px;
  display: flex;
  align-items: center;
  gap: 1rem;
  text-decoration: none;
  color: white;
  transition: all 0.3s ease;
  border: 2px solid rgba(255, 255, 255, 0.2);
}

.method-btn:hover {
  transform: translateY(-5px);
  background: rgba(255, 255, 255, 0.25);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.method-icon {
  font-size: 2.5rem;
}
.method-icon img {
  width: 42px;
  height: 42px;
  display: block;
  border-radius: 50%;
  object-fit: cover;
}

.method-name {
  font-weight: 700;
  font-size: 1.1rem;
}

.method-description {
  font-size: 0.875rem;
  opacity: 0.9;
}

.info-details {
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(10px);
  padding: 2rem;
  border-radius: 15px;
  border: 2px solid rgba(255, 255, 255, 0.2);
  color: white;
}

.detail-item {
  display: flex;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.detail-item:last-child {
  margin-bottom: 0;
}

.detail-icon {
  font-size: 1.5rem;
  flex-shrink: 0;
}


.contact-actions {
  display: flex;
  align-items: center;
}

.actions-card {
  background: white;
  padding: 2rem;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.18);
  width: 100%;
  text-align: center;
}

.call-btn {
  display: inline-block;
  padding: 1rem 1.5rem;
  font-size: 1.6rem;
  font-weight: 800;
  color: white;
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  border-radius: 12px;
  text-decoration: none;
  box-shadow: 0 8px 30px rgba(66,153,225,0.25);
}

.call-note {
  color: #718096;
  margin-top: 0.75rem;
}

.actions-methods {
  display: flex;
  gap: 0.75rem;
  justify-content: center;
  margin-top: 1rem;
}

.action-btn {
  padding: 0.6rem 1rem;
  border-radius: 10px;
  text-decoration: none;
  color: white;
  font-weight: 700;
}

.action-btn.whatsapp { background: #25D366 }
.action-btn.telegram { background: #2AABEE }

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.form-group {
  width: 100%;
}

.form-input {
  width: 100%;
  padding: 1rem 1.5rem;
  border: 2px solid #e2e8f0;
  border-radius: 12px;
  font-size: 1rem;
  transition: all 0.3s ease;
  font-family: inherit;
}

.form-input:focus {
  outline: none;
  border-color: #4299e1;
  box-shadow: 0 0 0 3px rgba(66, 153, 225, 0.1);
}

textarea.form-input {
  resize: vertical;
  min-height: 100px;
}

.submit-btn {
  padding: 1rem 2rem;
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  color: white;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 20px rgba(66, 153, 225, 0.4);
}

.submit-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 30px rgba(66, 153, 225, 0.5);
}

@media (max-width: 968px) {
  .contact-content {
    grid-template-columns: 1fr;
  }

  .contact-methods {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  .contact {
    padding: 4rem 0;
  }

  .section-title {
    font-size: 2rem;
  }

  .contact-content {
    grid-template-columns: 1fr;
  }

  .actions-card {
    padding: 1.25rem;
  }

  .call-btn {
    font-size: 1.25rem;
  }

  .phone-number {
    font-size: 1.5rem;
  }
}
</style>
