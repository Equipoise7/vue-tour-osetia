<script setup>
import { ref } from 'vue'
import Transfer from './Transfer.vue'
import Tours from './Tours.vue'

const activeTab = ref('transfer')

const tabs = [
  { id: 'transfer', name: 'Трансфер и перевозки', icon: '🚙' },
  { id: 'tours', name: 'Экскурсии по Осетии', icon: '🏔️' }
]

const switchTab = (tabId) => {
  activeTab.value = tabId
}
</script>

<template>
  <section id="services" class="services-tab">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Наши услуги</h2>
        <p class="section-subtitle">Выберите интересующий вас раздел</p>
      </div>

      <div class="tabs">
        <button
          v-for="tab in tabs"
          :key="tab.id"
          @click="switchTab(tab.id)"
          class="tab-button"
          :class="{ active: activeTab === tab.id }"
        >
          <span class="tab-icon">{{ tab.icon }}</span>
          <span class="tab-name">{{ tab.name }}</span>
        </button>
      </div>

      <div class="tab-content">
        <transition name="fade" mode="out-in">
          <Transfer v-if="activeTab === 'transfer'" key="transfer" />
          <Tours v-else-if="activeTab === 'tours'" key="tours" />
        </transition>
      </div>
    </div>
  </section>
</template>

<style scoped>
.services-tab {
  padding: 6rem 0;
  background: linear-gradient(135deg, #f7fafc 0%, #edf2f7 100%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section-header {
  text-align: center;
  margin-bottom: 3rem;
}

.section-title {
  font-size: 3rem;
  font-weight: 800;
  color: #2c5282;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, rgba(44, 82, 130, 0.7) 0%, rgba(66, 153, 225, 0.7) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-subtitle {
  font-size: 1.25rem;
  color: #4a5568;
}

.tabs {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
  position: relative;
}

.tabs::after {
  content: 'Кликните для выбора ☝️';
  position: absolute;
  bottom: -2.5rem;
  left: 50%;
  transform: translateX(-50%);
  font-size: 0.95rem;
  color: #4299e1;
  font-weight: 600;
  animation: bounce 2s ease-in-out infinite;
  white-space: nowrap;
}

@keyframes bounce {
  0%, 100% { 
    transform: translateX(-50%) translateY(0);
    opacity: 1;
  }
  50% { 
    transform: translateX(-50%) translateY(-8px);
    opacity: 0.7;
  }
}

.tab-button {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem 2.5rem;
  background: rgba(255, 255, 255, 0.6);
  backdrop-filter: blur(10px);
  border: 2px solid rgba(66, 153, 225, 0.2);
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 700;
  color: #4a5568;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
}

.tab-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 25px rgba(66, 153, 225, 0.2);
  border-color: rgba(66, 153, 225, 0.4);
}

.tab-button.active {
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  color: white;
  border-color: transparent;
  box-shadow: 0 8px 30px rgba(66, 153, 225, 0.4);
  transform: translateY(-5px);
}

.tab-icon {
  font-size: 1.5rem;
  transition: transform 0.3s ease;
}

.tab-button.active .tab-icon {
  transform: scale(1.2);
}

.tab-name {
  font-size: 1.1rem;
}

.tab-content {
  min-height: 400px;
}

/* Fade transition */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.fade-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.fade-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

@media (max-width: 768px) {
  .services-tab {
    padding: 4rem 0;
  }

  .section-title {
    font-size: 2rem;
  }

  .section-subtitle {
    font-size: 1.1rem;
  }

  .tabs::after {
    bottom: -2rem;
    font-size: 0.85rem;
  }

  .tabs {
    flex-direction: column;
    gap: 1rem;
  }

  .tab-button {
    width: 100%;
    justify-content: center;
    padding: 1.25rem 2rem;
  }

  .tab-name {
    font-size: 1rem;
  }
}
</style>
