<script setup>
const services = [
  {
    icon: '🏔️',
    title: 'Горные туры',
    description: 'Экскурсии по живописным ущельям: Цейское, Куртатинское, Дигорское, Кармадонское',
    features: ['Опытные гиды', 'Безопасность', 'Гибкий график']
  },
  {
    icon: '🚙',
    title: 'Трансфер',
    description: 'Комфортные перевозки на Toyota Alphard по республике и межгород',
    features: ['Комфорт класса люкс', 'До 7 пассажиров', 'Кондиционер']
  },
  {
    icon: '📸',
    title: 'Фототуры',
    description: 'Посещение самых красивых локаций для незабываемых фотографий',
    features: ['Лучшие виды', 'Помощь с фото', 'Уникальные места']
  },
  {
    icon: '🎿',
    title: 'Зимние туры',
    description: 'Горнолыжные курорты и зимние развлечения в горах Осетии',
    features: ['Цей ГЛК', 'Снежные пейзажи', 'Зимняя сказка']
  },
  {
    icon: '🏛️',
    title: 'Культурные экскурсии',
    description: 'Знакомство с историей, архитектурой и традициями Осетии',
    features: ['Древние башни', 'Музеи', 'Святилища']
  },
  {
    icon: '⭐',
    title: 'VIP туры',
    description: 'Индивидуальные маршруты с повышенным комфортом',
    features: ['Личный гид', 'Премиум сервис', 'Гибкая программа']
  }
]
</script>

<template>
  <section id="services" class="services">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Наши услуги</h2>
        <p class="section-subtitle">Откройте для себя всё разнообразие горной Осетии</p>
      </div>

      <div class="services-grid">
        <div 
          v-for="(service, index) in services" 
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
    </div>
  </section>
</template>

<style scoped>
.services {
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

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 2rem;
}

.service-card {
  background: white;
  padding: 2.5rem;
  border-radius: 20px;
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
  background: linear-gradient(90deg, #2c5282 0%, #4299e1 100%);
  transform: scaleX(0);
  transition: transform 0.4s ease;
}

.service-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 12px 40px rgba(44, 82, 130, 0.2);
}

.service-card:hover::before {
  transform: scaleX(1);
}

.service-icon {
  font-size: 3.5rem;
  margin-bottom: 1.5rem;
  display: inline-block;
  transition: transform 0.4s ease;
}

.service-card:hover .service-icon {
  transform: scale(1.1) rotate(5deg);
}

.service-title {
  font-size: 1.5rem;
  font-weight: 700;
  color: #2d3748;
  margin-bottom: 1rem;
}

.service-description {
  color: #4a5568;
  margin-bottom: 1.5rem;
  line-height: 1.6;
}

.service-features {
  list-style: none;
  padding: 0;
  margin: 0;
}

.service-features li {
  color: #4a5568;
  margin-bottom: 0.75rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.checkmark {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 20px;
  height: 20px;
  background: linear-gradient(135deg, #48bb78 0%, #38a169 100%);
  color: white;
  border-radius: 50%;
  font-size: 0.75rem;
  font-weight: bold;
  flex-shrink: 0;
}

@media (max-width: 768px) {
  .services {
    padding: 4rem 0;
  }

  .section-title {
    font-size: 2rem;
  }

  .section-subtitle {
    font-size: 1.1rem;
  }

  .services-grid {
    grid-template-columns: 1fr;
  }
}
</style>
