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
          <img src="/images/alphard.png" alt="Toyota Alphard" class="car-photo">
          <div class="car-overlay">
            <div class="car-label">Toyota Alphard</div>
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
  background: linear-gradient(135deg, rgba(44, 82, 130, 0.7) 0%, rgba(66, 153, 225, 0.7) 100%);
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
  /* фиксированная высота контейнера, чтобы изображение занимало всю рамку без пустот */
  height: 700px;
  border-radius: 30px;
  overflow: hidden;
  box-shadow: 0 20px 60px rgba(44, 82, 130, 0.3);
  transition: all 0.4s ease;
  animation: floatCar 4s ease-in-out infinite;
}

.transport-image:hover {
  box-shadow: 0 30px 80px rgba(44, 82, 130, 0.5);
}

@keyframes floatCar {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

.car-photo {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center 50%;
  display: block;
  transition: transform 0.3s ease, object-position 0.3s ease;
  z-index: 0;
}

.car-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(44, 82, 130, 0.15) 0%, rgba(66, 153, 225, 0.08) 100%);
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: space-between;
  padding: 2rem;
  transition: all 0.3s ease;
}

.transport-image:hover .car-overlay {
  background: linear-gradient(135deg, rgba(44, 82, 130, 0.25) 0%, rgba(66, 153, 225, 0.15) 100%);
}

.car-badge {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  color: #2c5282;
  padding: 0.75rem 1.5rem;
  border-radius: 50px;
  font-weight: 700;
  font-size: 1.1rem;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  animation: shimmer 3s ease-in-out infinite;
  align-self: flex-end;
}

@keyframes shimmer {
  0%, 100% {
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  }
  50% {
    box-shadow: 0 4px 30px rgba(66, 153, 225, 0.4), 0 0 20px rgba(66, 153, 225, 0.3);
  }
}

.car-label {
  font-size: 0.75rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.9);
  text-transform: uppercase;
  letter-spacing: 2px;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
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
  background: rgba(255, 255, 255, 0.6);
  backdrop-filter: blur(10px);
  border-radius: 15px;
  border: 1px solid rgba(66, 153, 225, 0.1);
  transition: all 0.3s ease;
}

.feature-item:hover {
  transform: translateX(10px);
  background: rgba(255, 255, 255, 0.9);
  box-shadow: 0 4px 20px rgba(66, 153, 225, 0.3);
  border-color: rgba(66, 153, 225, 0.3);
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

@media (max-width: 968px) {
  .transport-content {
    grid-template-columns: 1fr;
    gap: 3rem;
  }

  .features-grid {
    grid-template-columns: 1fr;
  }

  /* Настройки для планшетов: оставляем cover, но смещаем фокус ниже и немного поднимаем картинку */
  .car-photo {
    /* Убираем transform — оно создаёт пустое пространство внизу при смещении изображения */
    object-position: center 62%;
  }
}

@media (max-width: 768px) {
  .transport {
    padding: 4rem 0;
  }

  /* На телефонах ещё больше смещаем картинку вниз и уменьшаем высоту */
  .car-photo {
    /* Поднимем видимую область картинки за счёт object-position, без translate */
    object-position: center 68%;
  }

  .section-title {
    font-size: 2rem;
  }

  .info-title {
    font-size: 1.5rem;
  }
}
</style>
