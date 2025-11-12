<script setup>
import { ref } from 'vue'

const isMenuOpen = ref(false)

const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
    isMenuOpen.value = false
  }
}
</script>

<template>
  <header class="header">
    <div class="container">
      <div class="logo">
        <span class="logo-icon">⛰️</span>
        <span class="logo-text">Осетия Туры</span>
      </div>
      
      <button class="burger" @click="isMenuOpen = !isMenuOpen" :class="{ active: isMenuOpen }">
        <span></span>
        <span></span>
        <span></span>
      </button>

      <nav class="nav" :class="{ open: isMenuOpen }">
        <a @click="scrollToSection('hero')" class="nav-link">Главная</a>
        <a @click="scrollToSection('services')" class="nav-link">Услуги</a>
        <a @click="scrollToSection('gallery')" class="nav-link">Маршруты</a>
        <a @click="scrollToSection('transport')" class="nav-link">Транспорт</a>
        <a @click="scrollToSection('contact')" class="nav-link contact-btn">Связаться</a>
      </nav>
    </div>
  </header>
</template>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 1.5rem;
  font-weight: 700;
  color: #2c5282;
}

.logo-icon {
  font-size: 2rem;
}

.logo-text {
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.burger {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 5px;
}

.burger span {
  width: 25px;
  height: 3px;
  background: #2c5282;
  border-radius: 3px;
  transition: all 0.3s ease;
}

.burger.active span:nth-child(1) {
  transform: rotate(45deg) translate(7px, 7px);
}

.burger.active span:nth-child(2) {
  opacity: 0;
}

.burger.active span:nth-child(3) {
  transform: rotate(-45deg) translate(7px, -7px);
}

.nav {
  display: flex;
  gap: 2rem;
  align-items: center;
}

.nav-link {
  color: #2d3748;
  text-decoration: none;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  transition: width 0.3s ease;
}

.nav-link:hover::after {
  width: 100%;
}

.nav-link:hover {
  color: #4299e1;
}

.contact-btn {
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  color: white;
  padding: 0.75rem 1.5rem;
  border-radius: 50px;
  border: none;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(66, 153, 225, 0.3);
}

.contact-btn::after {
  display: none;
}

.contact-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(66, 153, 225, 0.4);
  color: white;
}

@media (max-width: 768px) {
  .burger {
    display: flex;
  }

  .nav {
    position: fixed;
    top: 70px;
    left: 0;
    right: 0;
    background: white;
    flex-direction: column;
    padding: 2rem;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    transform: translateY(-120%);
    transition: transform 0.3s ease;
  }

  .nav.open {
    transform: translateY(0);
  }
}
</style>
