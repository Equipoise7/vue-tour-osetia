<script setup>
const currentYear = new Date().getFullYear()
const phone = '+7 (989) 741-36-34'
const phoneClean = '79897413634'
</script>

<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-section">
          <div class="footer-logo">
            <span class="logo-icon">⛰️</span>
            <span class="logo-text">Осетия Туры</span>
          </div>
          <p class="footer-description">
            Профессиональные туры и трансферы по горам Северной Осетии. 
            Откройте для себя красоту Кавказа вместе с нами!
          </p>
          <div class="social-links">
            <a :href="`https://wa.me/${phoneClean}`" target="_blank" class="social-link whatsapp" title="WhatsApp">
              💬
            </a>
            <a :href="`https://t.me/${phoneClean}`" target="_blank" class="social-link telegram" title="Telegram">
              ✈️
            </a>
            <a :href="`tel:${phoneClean}`" class="social-link phone" title="Позвонить">
              📞
            </a>
          </div>
        </div>

        <div class="footer-section">
          <h4 class="footer-title">Наши услуги</h4>
          <ul class="footer-links">
            <li><a href="#services">Горные туры</a></li>
            <li><a href="#services">Трансфер межгород</a></li>
            <li><a href="#gallery">Фототуры</a></li>
            <li><a href="#services">Зимние туры</a></li>
            <li><a href="#services">Культурные экскурсии</a></li>
          </ul>
        </div>

        <div class="footer-section">
          <h4 class="footer-title">Популярные маршруты</h4>
          <ul class="footer-links">
            <li><a href="#gallery">Цейское ущелье</a></li>
            <li><a href="#gallery">Кармадонское ущелье</a></li>
            <li><a href="#gallery">Дигорское ущелье</a></li>
            <li><a href="#gallery">Куртатинское ущелье</a></li>
            <li><a href="#gallery">Даргавс</a></li>
          </ul>
        </div>

        <div class="footer-section">
          <h4 class="footer-title">Контакты</h4>
          <ul class="footer-contacts">
            <li>
              <span class="contact-icon">📞</span>
              <a :href="`tel:${phoneClean}`">{{ phone }}</a>
            </li>
            <li>
              <span class="contact-icon">✉️</span>
              <a href="mailto:Transfer15rus@yandex.ru">Transfer15rus@yandex.ru</a>
            </li>
            <li>
              <span class="contact-icon">📍</span>
              <span>г. Владикавказ, РСО-Алания</span>
            </li>
            <li>
              <span class="contact-icon">🕐</span>
              <span>Ежедневно 8:00 - 22:00</span>
            </li>
          </ul>
        </div>
      </div>

      <div class="footer-bottom">
        <div class="copyright">
          © {{ currentYear }} Осетия Туры. Все права защищены.
        </div>
        <div class="footer-note">
          Сделано с ❤️ для путешественников
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: linear-gradient(135deg, #1a365d 0%, #2c5282 100%);
  color: white;
  padding: 4rem 0 2rem;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.footer-content {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1.5fr;
  gap: 3rem;
  margin-bottom: 3rem;
}

.footer-section {
  display: flex;
  flex-direction: column;
}

.footer-logo {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
}

.logo-icon {
  font-size: 2rem;
}

.logo-text {
  background: linear-gradient(135deg, white 0%, #90cdf4 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.footer-description {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.social-links {
  display: flex;
  gap: 1rem;
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  text-decoration: none;
  font-size: 1.5rem;
  transition: all 0.3s ease;
  border: 2px solid rgba(255, 255, 255, 0.2);
}

.social-link:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(-5px) scale(1.1);
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
}

.footer-title {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  color: white;
}

.footer-links {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-links li {
  margin-bottom: 0.75rem;
}

.footer-links a {
  color: rgba(255, 255, 255, 0.8);
  text-decoration: none;
  transition: all 0.3s ease;
  display: inline-block;
}

.footer-links a:hover {
  color: white;
  transform: translateX(5px);
}

.footer-contacts {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-contacts li {
  display: flex;
  align-items: flex-start;
  gap: 0.5rem;
  margin-bottom: 1rem;
  color: rgba(255, 255, 255, 0.8);
}

.contact-icon {
  font-size: 1.2rem;
  flex-shrink: 0;
}

.footer-contacts a {
  color: rgba(255, 255, 255, 0.8);
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-contacts a:hover {
  color: white;
}

.footer-bottom {
  padding-top: 2rem;
  border-top: 1px solid rgba(255, 255, 255, 0.2);
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.copyright {
  color: rgba(255, 255, 255, 0.7);
}

.footer-note {
  color: rgba(255, 255, 255, 0.7);
}

@media (max-width: 968px) {
  .footer-content {
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
  }
}

@media (max-width: 768px) {
  .footer {
    padding: 3rem 0 1.5rem;
  }

  .footer-content {
    grid-template-columns: 1fr;
  }

  .footer-bottom {
    flex-direction: column;
    text-align: center;
  }

  .social-links {
    justify-content: center;
  }
}
</style>
