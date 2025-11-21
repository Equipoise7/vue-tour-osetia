<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isMenuOpen = ref(false)
const isScrolled = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
    isMenuOpen.value = false
  }
}
</script>

<template>
  <header class="header" :class="{ scrolled: isScrolled }">
    <div class="container">
      <div class="logo">
        <div class="flag-icon">
          <div class="flag-stripe white"></div>
          <div class="flag-stripe red"></div>
          <div class="flag-stripe yellow"></div>
        </div>
        <span class="logo-text">Туры Осетии</span>
      </div>
      
      <button class="burger" @click="isMenuOpen = !isMenuOpen" :class="{ active: isMenuOpen }">
        <span></span>
        <span></span>
        <span></span>
      </button>

      <nav class="nav" :class="{ open: isMenuOpen }">
        <a @click="scrollToSection('hero')" class="nav-link">Главная</a>
        <a @click="scrollToSection('services')" class="nav-link">Услуги</a>
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
  background: transparent;
  backdrop-filter: none;
  box-shadow: none;
  transition: all 0.3s ease;
  height: 70px;
}

.header.scrolled {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
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
  gap: 0.75rem;
  font-size: 1.5rem;
  font-weight: 700;
  color: white;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.8);
  transition: all 0.3s ease;
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.5));
}

.header.scrolled .logo {
  color: #2c5282;
  text-shadow: none;
  filter: none;
}

.flag-icon {
  width: 32px;
  height: 24px;
  display: flex;
  flex-direction: column;
  border-radius: 2px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  position: relative;
}

.flag-stripe {
  flex: 1;
  width: 100%;
  position: relative;
  animation: waveFlag 1.5s ease-in-out infinite;
}

.flag-stripe.white {
  background: linear-gradient(90deg, 
    #ffffff 0%, 
    #f0f0f0 25%, 
    #ffffff 50%, 
    #f0f0f0 75%, 
    #ffffff 100%
  );
  background-size: 200% 100%;
  animation: waveFlag 1.5s ease-in-out infinite, shimmer 3s linear infinite;
}

.flag-stripe.red {
  background: linear-gradient(90deg, 
    #ef4444 0%, 
    #dc2626 25%, 
    #ef4444 50%, 
    #dc2626 75%, 
    #ef4444 100%
  );
  background-size: 200% 100%;
  animation: waveFlag 1.5s ease-in-out infinite 0.1s, shimmer 3s linear infinite 0.1s;
}

.flag-stripe.yellow {
  background: linear-gradient(90deg, 
    #fbbf24 0%, 
    #f59e0b 25%, 
    #fbbf24 50%, 
    #f59e0b 75%, 
    #fbbf24 100%
  );
  background-size: 200% 100%;
  animation: waveFlag 1.5s ease-in-out infinite 0.2s, shimmer 3s linear infinite 0.2s;
}

@keyframes waveFlag {
  0%, 100% {
    transform: translateX(0) scaleX(1);
  }
  25% {
    transform: translateX(1px) scaleX(0.98);
  }
  50% {
    transform: translateX(0) scaleX(1.02);
  }
  75% {
    transform: translateX(-1px) scaleX(0.98);
  }
}

@keyframes shimmer {
  0% {
    background-position: 200% 0;
  }
  100% {
    background-position: -200% 0;
  }
}

.logo-text {
  color: #ffffff;
  font-weight: 700;
  transition: all 0.3s ease;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
}

.header.scrolled .logo-text {
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-shadow: none;
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
  background: white;
  border-radius: 3px;
  transition: all 0.3s ease;
}

.header.scrolled .burger span {
  background: #2c5282;
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
  color: white;
  text-decoration: none;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.8);
  filter: drop-shadow(0 1px 3px rgba(0, 0, 0, 0.5));
}

.header.scrolled .nav-link {
  color: #2d3748;
  text-shadow: none;
  filter: none;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: white;
  transition: width 0.3s ease;
}

.header.scrolled .nav-link::after {
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
}

.nav-link:hover::after {
  width: 100%;
}

.nav-link:hover {
  color: rgba(255, 255, 255, 0.8);
}

.header.scrolled .nav-link:hover {
  color: #4299e1;
}

.contact-btn {
  background: rgba(255, 255, 255, 0.15);
  color: white;
  padding: 0.75rem 1.5rem;
  border-radius: 50px;
  border: 2px solid rgba(255, 255, 255, 0.8);
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(10px);
}

.header.scrolled .contact-btn {
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  border: none;
  box-shadow: 0 4px 15px rgba(66, 153, 225, 0.3);
}

.contact-btn::after {
  display: none;
}

.contact-btn:hover {
  transform: translateY(-2px);
  background: white;
  color: #2c5282;
  box-shadow: 0 6px 20px rgba(255, 255, 255, 0.3);
}

.header.scrolled .contact-btn:hover {
  box-shadow: 0 6px 20px rgba(66, 153, 225, 0.4);
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
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
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(10px);
    flex-direction: column;
    padding: 2rem;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    transform: translateY(-100%);
    transition: transform 0.3s ease;
    opacity: 0;
    visibility: hidden;
  }

  .nav.open {
    transform: translateY(0);
    opacity: 1;
    visibility: visible;
  }

  .nav.open .nav-link {
    color: #2d3748;
    text-shadow: none;
  }
  
  .nav.open .contact-btn {
    background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
    border: none;
  }
}
</style>
