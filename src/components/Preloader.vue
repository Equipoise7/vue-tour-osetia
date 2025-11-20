<script setup>
import { ref, onMounted } from 'vue'

const isLoading = ref(true)

onMounted(() => {
  window.addEventListener('load', () => {
    setTimeout(() => {
      isLoading.value = false
    }, 500)
  })
})
</script>

<template>
  <transition name="fade">
    <div v-if="isLoading" class="preloader">
      <div class="preloader-content">
        <div class="logo-animation">
          <span class="mountain">⛰️</span>
          <h1 class="brand">Осетия Туры</h1>
        </div>
        <div class="loader">
          <div class="loader-bar"></div>
        </div>
      </div>
    </div>
  </transition>
</template>

<style scoped>
.preloader {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10000;
}

.preloader-content {
  text-align: center;
}

.logo-animation {
  margin-bottom: 2rem;
  animation: fadeInScale 0.8s ease-out;
}

.mountain {
  font-size: 5rem;
  display: block;
  margin-bottom: 1rem;
  animation: bounce 1.5s ease-in-out infinite;
}

.brand {
  font-size: 2.5rem;
  font-weight: 800;
  color: white;
  margin: 0;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  letter-spacing: 2px;
}

.loader {
  width: 200px;
  height: 4px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 10px;
  overflow: hidden;
  margin: 0 auto;
}

.loader-bar {
  height: 100%;
  background: linear-gradient(90deg, 
    rgba(255, 255, 255, 0.8) 0%, 
    rgba(255, 255, 255, 1) 50%, 
    rgba(255, 255, 255, 0.8) 100%);
  border-radius: 10px;
  animation: loading 1.5s ease-in-out infinite;
}

@keyframes fadeInScale {
  from {
    opacity: 0;
    transform: scale(0.8);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

@keyframes loading {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(200%);
  }
}

.fade-enter-active {
  transition: opacity 0.5s ease;
}

.fade-leave-active {
  transition: opacity 0.8s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 768px) {
  .mountain {
    font-size: 4rem;
  }

  .brand {
    font-size: 2rem;
  }

  .loader {
    width: 150px;
  }
}
</style>
