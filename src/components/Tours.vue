<script setup>
import { ref, computed, watch, onBeforeUnmount } from 'vue'

const selectedRoute = ref(null)
const currentPhotoIndex = ref(0)

const popularRoutes = [
  {
    id: 1,
    title: 'Золотое кольцо',
    description: 'Легендарный маршрут по главным достопримечательностям',
    video: '/videos/cards_videos/koleso.mp4',
    image: '/images/fiagdon.jpg',
    detailedDescription: `- ПАМЯТНИК ЖЕРТВАМ СХОДА ЛЕДНИКА КОЛКА
- ПРЕДПОЛОЖИТЕЛЬНОЕ МЕСТО ГИБЕЛИ СЪЕМОЧНОЙ ГРУППЫ БОДРОВА
- СМОТРОВАЯ ПЛОЩАДКА В СЕЛЕНИИ КАНИ
- ДАРГАВСКИЙ НЕКРОПОЛЬ (МЕРТВЫЙ ГОРОДОК)
- МИДАГРАБИНСКИЕ ВОДОПАДЫ
- БУКВА Æ
- КАЧЕЛИ НАД ОБРЫВОМ
- БАШНИ КУРТА И ТАГА
- АЛАНСКИЙ МУЖСКОЙ МОНАСТЫРЬ (САМЫЙ ВЫСОКОГОРНЫЙ МОНАСТЫРЬ)
- ДЗИВГИССКАЯ НАСКАЛЬНАЯ КРЕПОСТЬ
- КАДАРГАВАНСКИЙ КАНЬОН
- КАСКАДНЫЙ ВОДОПАД

ДОПОЛНИТЕЛЬНЫЕ ЛОКАЦИИ:
- лавочка счастья
- водопад кольцо

ЧТО ВХОДИТ В СТОИМОСТЬ ТУРА:
- услуги гида-экскурсовода на внедорожнике
- фото-видеосъемка 📹
- по желанию : перекус (мятный чай, осетинский сыр, хлеб)
- главное и основное : прекрасное настроение 😊

* Съемка с квадракоптера по запросу`,
    photos: [
      '/images/fiagdon.jpg',
      '/images/dargavs.jpg',
      '/images/ceiskoe.jpg'
    ]
  },
  {
    id: 2,
    title: 'Алагирское ущелье',
    description: 'Святилище Уастырджи и источники Тамиск',
    image: '/images/ozero.jpg',
    longDescription: 'Алагирское ущелье — одно из самых живописных мест Северной Осетии. Знаменитое святилище Уастырджи, высеченное в скале, и целебные источники Тамиск привлекают туристов со всего мира.',
    photos: [
      '/images/ozero.jpg',
      '/images/fiagdon.jpg'
    ]
  },
  {
    id: 3,
    title: 'Цейское ущелье',
    description: 'Горнолыжный курорт и ледники',
    image: '/images/ceiskoe.jpg',
    longDescription: 'Цейское ущелье - жемчужина Северной Осетии. Здесь расположен популярный горнолыжный курорт, величественные ледники и живописные горные вершины.',
    photos: [
      '/images/ceiskoe.jpg',
      '/images/digorya.jpg'
    ]
  },
  {
    id: 4,
    title: 'Куртатинское ущелье',
    description: 'Каньон Кадаргаван и древние башни',
    image: '/images/kurtatinskoe.jpg',
    longDescription: 'Куртатинское ущелье славится своими древними башнями, Кадаргаванским каньоном и богатой историей. Это место, где можно прикоснуться к истории Алании.',
    photos: [
      '/images/kurtatinskoe.jpg',
      '/images/dargavs.jpg'
    ]
  },
  {
    id: 5,
    title: 'Дигорское ущелье',
    description: 'Замок-фрегат и каньон Ахсинта',
    image: '/images/digorya.jpg',
    longDescription: 'Дигорское ущелье удивляет своими пейзажами: замок-фрегат, каньон Ахсинта и нетронутая природа. Идеальное место для фотографий и единения с природой.',
    photos: [
      '/images/digorya.jpg',
      '/images/ceiskoe.jpg'
    ]
  },
  {
    id: 6,
    title: 'Даргавское ущелье',
    description: 'Город мертвых и Мидаграбинские водопады',
    image: '/images/dargavs.jpg',
    longDescription: 'Даргавское ущелье известно своим древним некрополем "Город мертвых" и величественными Мидаграбинскими водопадами. Мистическое и завораживающее место.',
    photos: [
      '/images/dargavs.jpg',
      '/images/fiagdon.jpg'
    ]
  }
]

const openRoute = (route) => {
  selectedRoute.value = route
  currentPhotoIndex.value = 0
}

const closeRoute = () => {
  selectedRoute.value = null
}

const selectedPhoto = computed(() => {
  if (!selectedRoute.value) return ''
  if (selectedRoute.value.photos?.length) {
    return selectedRoute.value.photos[currentPhotoIndex.value]
  }
  return selectedRoute.value.image
})

const nextPhoto = () => {
  if (!selectedRoute.value?.photos) return
  currentPhotoIndex.value = (currentPhotoIndex.value + 1) % selectedRoute.value.photos.length
}

const prevPhoto = () => {
  if (!selectedRoute.value?.photos) return
  currentPhotoIndex.value = (currentPhotoIndex.value - 1 + selectedRoute.value.photos.length) % selectedRoute.value.photos.length
}

const goToPhoto = (i) => {
  if (!selectedRoute.value?.photos) return
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

watch(selectedRoute, (val) => {
  val ? lockScroll() : unlockScroll()
})

onBeforeUnmount(() => {
  unlockScroll()
})
</script>

<template>
  <div class="tours">
    <!-- Блок популярных маршрутов -->
    <div class="routes-section">
      <h3 class="routes-title">Популярные маршруты</h3>
      <p class="routes-subtitle">Исследуйте красоту горных ущелий Северной Осетии</p>
      <div class="routes-grid">
        <div
          v-for="route in popularRoutes"
          :key="route.id"
          class="route-card"
          @click="openRoute(route)"
        >
          <video 
            v-if="route.video"
            class="route-video"
            :src="route.video"
            autoplay
            loop
            muted
            playsinline
            preload="metadata"
          ></video>
          <div 
            v-else
            class="route-image"
            :style="{ 
              backgroundImage: `url(${route.image})`,
              backgroundSize: 'cover',
              backgroundPosition: 'center'
            }"
          ></div>
          <div class="route-overlay">
            <h4 class="route-title">{{ route.title }}</h4>
            <p class="route-description">{{ route.description }}</p>
            <div class="view-icon">👁️</div>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal -->
    <transition name="modal">
      <div v-if="selectedRoute" class="modal" @click="closeRoute">
        <div class="modal-content" @click.stop>
          <button class="close-btn" @click="closeRoute">&times;</button>
          <div class="modal-body">
            <div class="modal-gallery">
              <button v-if="selectedRoute.photos && selectedRoute.photos.length > 1" class="nav-arrow left" @click="prevPhoto">‹</button>
              <div
                class="modal-main-image"
                :style="{
                  backgroundImage: `url(${selectedPhoto})`,
                  backgroundSize: 'cover',
                  backgroundPosition: 'center'
                }"
              ></div>
              <button v-if="selectedRoute.photos && selectedRoute.photos.length > 1" class="nav-arrow right" @click="nextPhoto">›</button>
            </div>

            <div class="modal-info">
              <h2 class="modal-title">{{ selectedRoute.title }}</h2>
              <p v-if="selectedRoute.detailedDescription" class="modal-description detailed" v-html="selectedRoute.detailedDescription.replace(/\n/g, '<br>')"></p>
              <p v-else class="modal-description">{{ selectedRoute.longDescription || selectedRoute.description }}</p>
              <div v-if="selectedRoute.photos && selectedRoute.photos.length > 1" class="modal-thumbs">
                <img
                  v-for="(p, idx) in selectedRoute.photos"
                  :key="idx"
                  :src="p"
                  :class="{ active: idx === currentPhotoIndex }"
                  @click="goToPhoto(idx)"
                  alt="thumbnail"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<style scoped>
.tours {
  animation: fadeIn 0.5s ease;
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

/* Блок популярных маршрутов */
.routes-section {
  padding: 0;
}

.routes-title {
  font-size: 2rem;
  font-weight: 800;
  color: #2d3748;
  text-align: center;
  margin-bottom: 0.5rem;
}

.routes-subtitle {
  font-size: 1.1rem;
  color: #4a5568;
  text-align: center;
  margin-bottom: 2.5rem;
}

.routes-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.route-card {
  position: relative;
  aspect-ratio: 9 / 16;
  border-radius: 20px;
  overflow: hidden;
  cursor: pointer;
  transition: all 0.4s ease;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

.route-video,
.route-image {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.route-video {
  pointer-events: none;
}

.route-card:hover {
  transform: translateY(-10px) scale(1.02);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
}

.route-overlay {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  background: rgba(0, 0, 0, 0.3);
  color: white;
  transition: all 0.4s ease;
}

.route-card:hover .route-overlay {
  background: rgba(0, 0, 0, 0.15);
}

.route-title {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  text-align: center;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
}

.route-description {
  font-size: 1rem;
  text-align: center;
  opacity: 0.95;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.5);
}

.view-icon {
  font-size: 2rem;
  margin-top: 1rem;
  opacity: 0;
  transform: scale(0);
  transition: all 0.4s ease;
}

.route-card:hover .view-icon {
  opacity: 1;
  transform: scale(1);
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
}

.modal-title {
  font-size: 2.5rem;
  font-weight: 800;
  margin-bottom: 1rem;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
}

.modal-description {
  font-size: 1.2rem;
  line-height: 1.6;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
}

.modal-description.detailed {
  font-size: 1rem;
  line-height: 1.8;
  text-align: left;
  white-space: pre-line;
  max-height: 450px;
  overflow-y: auto;
  padding-right: 1rem;
}

.modal-description.detailed::-webkit-scrollbar {
  width: 6px;
}

.modal-description.detailed::-webkit-scrollbar-track {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
}

.modal-description.detailed::-webkit-scrollbar-thumb {
  background: rgba(66, 153, 225, 0.6);
  border-radius: 10px;
}

.modal-description.detailed::-webkit-scrollbar-thumb:hover {
  background: rgba(66, 153, 225, 0.8);
}

.modal-thumbs {
  display: flex;
  gap: 0.5rem;
  margin-top: 1.5rem;
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
  .routes-grid {
    grid-template-columns: repeat(2, 1fr);
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
    font-size: 1rem;
  }
}

@media (max-width: 768px) {
  .routes-title {
    font-size: 1.5rem;
  }

  .routes-subtitle {
    font-size: 1rem;
  }

  .routes-grid {
    grid-template-columns: 1fr;
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

  .modal-title {
    font-size: 1.5rem;
  }

  .modal-description {
    font-size: 0.95rem;
  }

  .modal-description.detailed {
    max-height: 300px;
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
