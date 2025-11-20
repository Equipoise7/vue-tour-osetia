<script setup>
const transferServices = [
  {
    icon: '🚙',
    title: 'Комфортные поездки',
    description: 'Перевозки по городу и межгород на премиальном автомобиле',
    features: ['По Владикавказу', 'По всей России', 'Комфорт класса люкс']
  },
  {
    icon: '✈️',
    title: 'Аэропорт и вокзал',
    description: 'Встречи и проводы с табличкой, помощь с багажом',
    features: ['Встреча с табличкой', 'Помощь с багажом', 'Точность по времени']
  },
  {
    icon: '🏨',
    title: 'Отель и гостиницы',
    description: 'Трансфер до любого отеля или гостиницы',
    features: ['Быстрая подача', 'Удобный маршрут', 'Фиксированная цена']
  },
  {
    icon: '💼',
    title: 'Корпоративные перевозки',
    description: 'Для деловых встреч и корпоративных мероприятий',
    features: ['Надёжность', 'Пунктуальность', 'Конфиденциальность']
  }
]

const carFeatures = [
  'Премиум класс комфорта',
  'Просторный салон для 7 пассажиров',
  'Климат-контроль',
  'Кожаные сидения',
  'Панорамная крыша',
  'Современная аудиосистема'
]
</script>

<template>
  <div class="transfer">
    <div class="services-grid">
      <div 
        v-for="(service, index) in transferServices" 
        :key="index"
        class="service-card"
      >
        <div class="service-icon">{{ service.icon }}</div>
        <h3 class="service-title">{{ service.title }}</h3>
        <p class="service-description">{{ service.description }}</p>
        <ul class="service-features">
          <li v-for="(feature, i) in service.features" :key="i">
            <span class="checkmark">✓</span> {{ feature }}
          </li>
        </ul>
      </div>
    </div>

    <!-- Блок с машиной -->
    <div class="car-section">
      <div class="car-content">
        <div class="car-image">
          <img src="/images/alphard.png" alt="Toyota Alphard" class="car-photo">
          <div class="car-overlay">
            <div class="car-label">Toyota Alphard</div>
            <div class="car-badge">Premium</div>
          </div>
        </div>

        <div class="car-info">
          <h3 class="info-title">Наш автомобиль</h3>
          <p class="info-description">
            Toyota Alphard - премиальный минивэн для комфортных перевозок. 
            Идеально подходит для трансферов, деловых поездок и корпоративных перевозок.
          </p>

          <ul class="car-features-list">
            <li v-for="(feature, index) in carFeatures" :key="index">
              <span class="checkmark">✓</span> {{ feature }}
            </li>
          </ul>

          <div class="car-cta">
            <a href="#contact" class="cta-btn">Заказать трансфер</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.transfer {
  animation: fadeIn 0.5s ease;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.service-card {
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(10px);
  padding: 2rem;
  border-radius: 20px;
  border: 1px solid rgba(66, 153, 225, 0.1);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  transition: all 0.4s ease;
  position: relative;
  overflow: hidden;
}

.service-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 4px;
  background: linear-gradient(90deg, rgba(44, 82, 130, 0.6) 0%, rgba(66, 153, 225, 0.6) 100%);
  transform: scaleX(0);
  transition: transform 0.4s ease;
}

.service-card:hover {
  transform: translateY(-10px);
  background: rgba(255, 255, 255, 0.9);
  box-shadow: 0 12px 40px rgba(44, 82, 130, 0.2);
  border-color: rgba(66, 153, 225, 0.3);
}

.service-card:hover::before {
  transform: scaleX(1);
}

.service-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
  display: inline-block;
  transition: transform 0.4s ease;
}

.service-card:hover .service-icon {
  transform: scale(1.1) rotate(5deg);
}

.service-title {
  font-size: 1.35rem;
  font-weight: 700;
  color: #2d3748;
  margin-bottom: 0.75rem;
}

.service-description {
  color: #4a5568;
  margin-bottom: 1.25rem;
  line-height: 1.6;
  font-size: 0.95rem;
}

.service-features {
  list-style: none;
  padding: 0;
  margin: 0;
}

.service-features li {
  color: #4a5568;
  margin-bottom: 0.6rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.9rem;
}

.checkmark {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 18px;
  height: 18px;
  background: linear-gradient(135deg, #48bb78 0%, #38a169 100%);
  color: white;
  border-radius: 50%;
  font-size: 0.7rem;
  font-weight: bold;
  flex-shrink: 0;
}

/* Блок с машиной */
.car-section {
  margin-top: 4rem;
  padding-top: 4rem;
  border-top: 2px solid rgba(66, 153, 225, 0.1);
}

.car-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  align-items: center;
}

.car-image {
  position: relative;
  height: 500px;
  border-radius: 30px;
  overflow: hidden;
  box-shadow: 0 20px 60px rgba(44, 82, 130, 0.3);
  transition: all 0.4s ease;
  animation: floatCar 4s ease-in-out infinite;
}

.car-image:hover {
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
  object-position: center 65%;
  display: block;
  transition: transform 0.3s ease;
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

.car-image:hover .car-overlay {
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

.car-info {
  padding: 1rem 0;
}

.info-title {
  font-size: 2rem;
  font-weight: 800;
  color: #2d3748;
  margin-bottom: 1rem;
}

.info-description {
  font-size: 1.05rem;
  color: #4a5568;
  line-height: 1.7;
  margin-bottom: 2rem;
}

.car-features-list {
  list-style: none;
  padding: 0;
  margin: 0 0 2rem 0;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 0.75rem;
}

.car-features-list li {
  color: #4a5568;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.95rem;
}

.car-cta {
  margin-top: 1.5rem;
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

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 968px) {
  .car-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .car-features-list {
    grid-template-columns: 1fr;
  }

  .car-image {
    height: 450px;
  }

  .car-photo {
    object-position: center 70%;
  }
}

@media (max-width: 768px) {
  .services-grid {
    grid-template-columns: 1fr;
  }

  .car-section {
    margin-top: 3rem;
    padding-top: 3rem;
  }

  .car-image {
    height: 400px;
  }

  .car-photo {
    object-position: center 75%;
  }

  .info-title {
    font-size: 1.5rem;
  }

  .info-description {
    font-size: 0.95rem;
  }
}
</style>
