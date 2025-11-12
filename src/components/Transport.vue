<script setup>
const features = [
  {
    icon: '👥',
    title: 'До 7 пассажиров',
    description: 'Комфортабельные кожаные сиденья'
  },
  {
    icon: '❄️',
    title: 'Климат-контроль',
    description: 'Идеальная температура в любой сезон'
  },
  {
    icon: '🎵',
    title: 'Премиум аудиосистема',
    description: 'Качественный звук в дороге'
  },
  {
    icon: '📱',
    title: 'USB зарядка',
    description: 'Зарядка для всех устройств'
  },
  {
    icon: '🛡️',
    title: 'Безопасность',
    description: 'Современные системы безопасности'
  },
  {
    icon: '🧳',
    title: 'Багажное отделение',
    description: 'Место для всего необходимого'
  }
]
</script>

<template>
  <section id="transport" class="transport">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Наш транспорт</h2>
        <p class="section-subtitle">Toyota Alphard - комфорт премиум класса</p>
      </div>

      <div class="transport-content">
        <div class="transport-image">
          <div class="car-placeholder">
            <div class="car-icon">🚙</div>
            <div class="car-name">Toyota Alphard</div>
            <div class="car-badge">Premium</div>
          </div>
        </div>

        <div class="transport-info">
          <h3 class="info-title">Путешествуйте с комфортом</h3>
          <p class="info-description">
            Наш минивэн Toyota Alphard обеспечит максимальный комфорт во время поездки по горным маршрутам. 
            Просторный салон, мягкие кожаные сиденья и современное оснащение сделают вашу поездку незабываемой.
          </p>

          <div class="features-grid">
            <div v-for="(feature, index) in features" :key="index" class="feature-item">
              <div class="feature-icon">{{ feature.icon }}</div>
              <div class="feature-content">
                <h4 class="feature-title">{{ feature.title }}</h4>
                <p class="feature-description">{{ feature.description }}</p>
              </div>
            </div>
          </div>

          <div class="transport-cta">
            <a href="#contact" class="cta-btn">Забронировать трансфер</a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.transport {
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
  margin-bottom: 4rem;
}

.section-title {
  font-size: 3rem;
  font-weight: 800;
  color: #2c5282;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-subtitle {
  font-size: 1.25rem;
  color: #4a5568;
}

.transport-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.transport-image {
  position: relative;
}

.car-placeholder {
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  border-radius: 30px;
  padding: 4rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 400px;
  box-shadow: 0 20px 60px rgba(44, 82, 130, 0.3);
  position: relative;
  overflow: hidden;
}

.car-placeholder::before {
  content: '';
  position: absolute;
  top: -50%;
  right: -50%;
  width: 200%;
  height: 200%;
  background: linear-gradient(45deg, transparent 30%, rgba(255, 255, 255, 0.1) 50%, transparent 70%);
  animation: shine 3s infinite;
}

.car-icon {
  font-size: 8rem;
  margin-bottom: 1.5rem;
  animation: float 3s ease-in-out infinite;
}

.car-name {
  font-size: 2rem;
  font-weight: 800;
  color: white;
  margin-bottom: 1rem;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}

.car-badge {
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(10px);
  color: white;
  padding: 0.5rem 1.5rem;
  border-radius: 50px;
  font-weight: 700;
  border: 2px solid rgba(255, 255, 255, 0.3);
}

.transport-info {
  padding: 2rem 0;
}

.info-title {
  font-size: 2rem;
  font-weight: 800;
  color: #2d3748;
  margin-bottom: 1.5rem;
}

.info-description {
  font-size: 1.1rem;
  color: #4a5568;
  line-height: 1.8;
  margin-bottom: 2.5rem;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
  margin-bottom: 2.5rem;
}

.feature-item {
  display: flex;
  gap: 1rem;
  padding: 1rem;
  background: white;
  border-radius: 15px;
  transition: all 0.3s ease;
}

.feature-item:hover {
  transform: translateX(10px);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

.feature-icon {
  font-size: 2rem;
  flex-shrink: 0;
}

.feature-content {
  flex: 1;
}

.feature-title {
  font-size: 1rem;
  font-weight: 700;
  color: #2d3748;
  margin-bottom: 0.25rem;
}

.feature-description {
  font-size: 0.875rem;
  color: #718096;
}

.transport-cta {
  margin-top: 2rem;
}

.cta-btn {
  display: inline-block;
  padding: 1rem 2.5rem;
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  color: white;
  text-decoration: none;
  border-radius: 50px;
  font-weight: 700;
  font-size: 1.1rem;
  box-shadow: 0 4px 20px rgba(66, 153, 225, 0.4);
  transition: all 0.3s ease;
}

.cta-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 30px rgba(66, 153, 225, 0.5);
}

@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

@keyframes shine {
  0% {
    transform: translateX(-100%) translateY(-100%) rotate(45deg);
  }
  100% {
    transform: translateX(100%) translateY(100%) rotate(45deg);
  }
}

@media (max-width: 968px) {
  .transport-content {
    grid-template-columns: 1fr;
    gap: 3rem;
  }

  .features-grid {
    grid-template-columns: 1fr;
  }

  .car-placeholder {
    min-height: 350px;
  }

  .car-icon {
    font-size: 6rem;
  }
}

@media (max-width: 768px) {
  .transport {
    padding: 4rem 0;
  }

  .section-title {
    font-size: 2rem;
  }

  .info-title {
    font-size: 1.5rem;
  }
}
</style>
