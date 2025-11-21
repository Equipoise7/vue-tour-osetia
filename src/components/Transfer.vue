<script setup>
import { ref, computed, watch, onBeforeUnmount } from 'vue'

const selectedService = ref(null)
const currentPhotoIndex = ref(0)

const transferServices = [
  {
    icon: '🚙',
    title: 'Комфортные поездки',
    description: 'Перевозки по городу и межгород на премиальном автомобиле',
    features: ['По Владикавказу', 'По всей России', 'Комфорт класса люкс'],
    detailedDescription: `Предлагаем комфортабельные поездки на премиальном автомобиле Toyota Alphard.

✓ Поездки по Владикавказу
✓ Межгородские перевозки по всей России
✓ Комфорт класса люкс
✓ Опытные водители
✓ Чистый и ухоженный автомобиль
✓ Кондиционер и мультимедиа
✓ Возможность остановок по маршруту

Идеально подходит для деловых поездок, семейных путешествий и комфортного передвижения по городу.`,
    photos: [
      '/images/alphard.png',
      '/images/fiagdon.jpg'
    ]
  },
  {
    icon: '✈️',
    title: 'Аэропорт и вокзал',
    description: 'Встречи и проводы с табличкой, помощь с багажом',
    features: ['Встреча с табличкой', 'Помощь с багажом', 'Точность по времени'],
    detailedDescription: `Профессиональный сервис встречи и проводов в аэропорту и на вокзале.

✓ Встреча с именной табличкой
✓ Помощь с багажом
✓ Отслеживание рейсов
✓ Пунктуальность и точность
✓ Комфортное ожидание
✓ Прямая связь с водителем
✓ Фиксированная цена без доплат

Встретим вас или ваших гостей с максимальным комфортом в любое время суток.`,
    photos: [
      '/images/alphard.png',
      '/images/ozero.jpg'
    ]
  },
  {
    icon: '🏨',
    title: 'Отель и гостиницы',
    description: 'Трансфер до любого отеля или гостиницы',
    features: ['Быстрая подача', 'Удобный маршрут', 'Фиксированная цена'],
    detailedDescription: `Трансфер до отелей и гостиниц Владикавказа и пригорода.

✓ Быстрая подача автомобиля
✓ Оптимальный маршрут
✓ Фиксированная стоимость
✓ Просторный багажник
✓ Помощь с вещами
✓ Информация о городе от водителя
✓ Безналичная оплата

Доставим вас в отель быстро, комфортно и безопасно.`,
    photos: [
      '/images/alphard.png',
      '/images/ceiskoe.jpg'
    ]
  },
  {
    icon: '💼',
    title: 'Корпоративные перевозки',
    description: 'Для деловых встреч и корпоративных мероприятий',
    features: ['Надёжность', 'Пунктуальность', 'Конфиденциальность'],
    detailedDescription: `Корпоративные перевозки для деловых людей и компаний.

✓ Абсолютная надёжность
✓ Пунктуальность до минуты
✓ Конфиденциальность
✓ Представительский класс
✓ Деловая атмосфера
✓ Возможность работы в дороге
✓ Регулярные перевозки со скидкой
✓ Документы для бухгалтерии

Идеальное решение для деловых встреч, переговоров и корпоративных мероприятий.`,
    photos: [
      '/images/alphard.png',
      '/images/dargavs.jpg'
    ]
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

const openService = (service) => {
  selectedService.value = service
  currentPhotoIndex.value = 0
}

const closeService = () => {
  selectedService.value = null
}

const selectedPhoto = computed(() => {
  if (!selectedService.value) return ''
  if (selectedService.value.photos?.length) {
    return selectedService.value.photos[currentPhotoIndex.value]
  }
  return '/images/alphard.png'
})

const nextPhoto = () => {
  if (!selectedService.value?.photos) return
  currentPhotoIndex.value = (currentPhotoIndex.value + 1) % selectedService.value.photos.length
}

const prevPhoto = () => {
  if (!selectedService.value?.photos) return
  currentPhotoIndex.value = (currentPhotoIndex.value - 1 + selectedService.value.photos.length) % selectedService.value.photos.length
}

const goToPhoto = (i) => {
  if (!selectedService.value?.photos) return
  currentPhotoIndex.value = i
}

const lockScroll = () => {
  const scrollY = window.scrollY || window.pageYOffset || 0
  document.body.dataset.scrollY = String(scrollY)
  document.body.style.position = 'fixed'
  document.body.style.top = `-${scrollY}px`
  document.body.style.left = '0'
  document.body.style.right = '0'
  document.body.style.width = '100%'
}

const unlockScroll = () => {
  const stored = document.body.dataset.scrollY || '0'
  document.body.style.position = ''
  document.body.style.top = ''
  document.body.style.left = ''
  document.body.style.right = ''
  document.body.style.width = ''
  const scrollY = parseInt(stored, 10) || 0
  window.scrollTo(0, scrollY)
  delete document.body.dataset.scrollY
}

watch(selectedService, (val) => {
  val ? lockScroll() : unlockScroll()
})

onBeforeUnmount(() => {
  if (selectedService.value) {
    unlockScroll()
  }
})
</script>

<template>
  <div class="transfer">
    <div class="services-grid">
      <div 
        v-for="(service, index) in transferServices" 
        :key="index"
        class="service-card"
        @click="openService(service)"
      >
        <div class="service-icon">{{ service.icon }}</div>
        <h3 class="service-title">{{ service.title }}</h3>
        <p class="service-description">{{ service.description }}</p>
        <ul class="service-features">
          <li v-for="(feature, i) in service.features" :key="i">
            <span class="checkmark">✓</span> {{ feature }}
          </li>
        </ul>
        <div class="view-more">Подробнее →</div>
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

    <!-- Modal -->
    <transition name="modal">
      <div v-if="selectedService" class="modal" @click="closeService">
        <div class="modal-content" @click.stop>
          <button class="close-btn" @click="closeService">&times;</button>
          <div class="modal-body">
            <div class="modal-gallery">
              <button v-if="selectedService.photos && selectedService.photos.length > 1" class="nav-arrow left" @click="prevPhoto">‹</button>
              <div
                class="modal-main-image"
                :style="{
                  backgroundImage: `url(${selectedPhoto})`,
                  backgroundSize: 'cover',
                  backgroundPosition: 'center'
                }"
              ></div>
              <button v-if="selectedService.photos && selectedService.photos.length > 1" class="nav-arrow right" @click="nextPhoto">›</button>
            </div>

            <div class="modal-info">
              <div class="modal-icon">{{ selectedService.icon }}</div>
              <h2 class="modal-title">{{ selectedService.title }}</h2>
              <p class="modal-description" v-html="selectedService.detailedDescription.replace(/\n/g, '<br>')"></p>
              <div v-if="selectedService.photos && selectedService.photos.length > 1" class="modal-thumbs">
                <img
                  v-for="(p, idx) in selectedService.photos"
                  :key="idx"
                  :src="p"
                  :class="{ active: idx === currentPhotoIndex }"
                  @click="goToPhoto(idx)"
                  alt="thumbnail"
                />
              </div>
              <a href="#contact" class="modal-cta-btn" @click="closeService">Заказать</a>
            </div>
          </div>
        </div>
      </div>
    </transition>
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

.view-more {
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid rgba(66, 153, 225, 0.2);
  color: #4299e1;
  font-weight: 600;
  font-size: 0.95rem;
  text-align: center;
  opacity: 0;
  transform: translateY(-10px);
  transition: all 0.3s ease;
}

.service-card:hover .view-more {
  opacity: 1;
  transform: translateY(0);
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

/* Modal */
.modal {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.9);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
  padding: 2rem;
}

.modal-content {
  position: relative;
  max-width: 900px;
  width: 100%;
  animation: modalZoom 0.3s ease;
}

.close-btn {
  position: absolute;
  top: -50px;
  right: 0;
  background: none;
  border: none;
  color: white;
  font-size: 3rem;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 10;
}

.close-btn:hover {
  transform: rotate(90deg);
  color: #4299e1;
}

.modal-body {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
}

.modal-gallery {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-main-image {
  width: 100%;
  height: 500px;
  border-radius: 20px;
  background-size: cover;
  background-position: center;
  box-shadow: 0 10px 40px rgba(0,0,0,0.5);
}

.nav-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255,255,255,0.9);
  border: none;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  font-size: 2rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 6px 20px rgba(0,0,0,0.2);
  transition: all 0.3s ease;
}

.nav-arrow:hover {
  background: #4299e1;
  color: white;
}

.nav-arrow.left { left: -24px; }
.nav-arrow.right { right: -24px; }

.modal-info {
  color: #edf2f7;
  display: flex;
  flex-direction: column;
}

.modal-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.modal-title {
  font-size: 2.5rem;
  font-weight: 800;
  margin-bottom: 1.5rem;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
}

.modal-description {
  font-size: 1rem;
  line-height: 1.8;
  text-align: left;
  white-space: pre-line;
  max-height: 350px;
  overflow-y: auto;
  padding-right: 1rem;
  margin-bottom: 1.5rem;
  flex: 1;
}

.modal-description::-webkit-scrollbar {
  width: 6px;
}

.modal-description::-webkit-scrollbar-track {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
}

.modal-description::-webkit-scrollbar-thumb {
  background: rgba(66, 153, 225, 0.6);
  border-radius: 10px;
}

.modal-description::-webkit-scrollbar-thumb:hover {
  background: rgba(66, 153, 225, 0.8);
}

.modal-thumbs {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
  flex-wrap: wrap;
}

.modal-thumbs img {
  width: 80px;
  height: 60px;
  object-fit: cover;
  border-radius: 8px;
  cursor: pointer;
  opacity: 0.6;
  border: 2px solid transparent;
  transition: all 0.3s ease;
}

.modal-thumbs img:hover {
  opacity: 0.8;
}

.modal-thumbs img.active {
  opacity: 1;
  border-color: #4299e1;
}

.modal-cta-btn {
  display: inline-block;
  padding: 1rem 2.5rem;
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
  color: white;
  text-decoration: none;
  border-radius: 50px;
  font-weight: 700;
  font-size: 1.1rem;
  text-align: center;
  box-shadow: 0 4px 20px rgba(66, 153, 225, 0.4);
  transition: all 0.3s ease;
}

.modal-cta-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 30px rgba(66, 153, 225, 0.5);
}

.modal-enter-active, .modal-leave-active {
  transition: opacity 0.3s ease;
}

.modal-enter-from, .modal-leave-to {
  opacity: 0;
}

@keyframes modalZoom {
  from {
    transform: scale(0.8);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
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

  .modal-body {
    display: block;
  }

  .modal-gallery {
    margin-bottom: 1rem;
  }

  .modal-main-image {
    height: 350px;
  }

  .modal-title {
    font-size: 1.8rem;
  }

  .modal-description {
    font-size: 0.95rem;
    max-height: 250px;
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

  .modal {
    padding: 1rem;
  }

  .close-btn {
    top: -40px;
    font-size: 2.5rem;
  }

  .modal-main-image {
    height: 300px;
    border-radius: 12px;
  }

  .nav-arrow {
    display: none;
  }

  .modal-icon {
    font-size: 2rem;
  }

  .modal-title {
    font-size: 1.5rem;
  }

  .modal-description {
    font-size: 0.9rem;
    max-height: 200px;
  }

  .modal-thumbs {
    gap: 0.5rem;
    overflow-x: auto;
    padding-bottom: 0.5rem;
  }

  .modal-thumbs img {
    width: 64px;
    height: 48px;
  }
}
</style>
