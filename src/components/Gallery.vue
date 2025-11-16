<script setup>
import { ref, computed, watch, onBeforeUnmount } from 'vue'

const activeCategory = ref('all')
const selectedImage = ref(null)

const categories = [
  { id: 'all', name: 'Все' },
  { id: 'mountains', name: 'Горы' },
  { id: 'gorges', name: 'Ущелья' },
  { id: 'winter', name: 'Зима' },
  { id: 'culture', name: 'Культура' }
]

const images = [
  {
    id: 1,
    category: 'gorges',
    title: 'Дарьяльское ущелье',
    description: 'Ворота Кавказа на Военно-Грузинской дороге',
    image: '/vue-tour-osetia/images/fiagdon.jpg',
    color: '#4299e1'
  },
  {
    id: 2,
    category: 'gorges',
    title: 'Алагирское ущелье',
    description: 'Святилище Уастырджи и источники Тамиск',
    image: '/vue-tour-osetia/images/ozero.jpg',
    color: '#48bb78'
  },
  {
    id: 3,
    category: 'mountains',
    title: 'Цейское ущелье',
    description: 'Горнолыжный курорт и ледники',
    image: '/vue-tour-osetia/images/ceiskoe.jpg',
    color: '#ed8936'
  },
  {
    id: 4,
    category: 'gorges',
    title: 'Куртатинское ущелье',
    description: 'Каньон Кадаргаван и древние башни',
    image: '/vue-tour-osetia/images/kurtatinskoe.jpg',
    color: '#667eea'
  },
  {
    id: 5,
    category: 'mountains',
    title: 'Дигорское ущелье',
    description: 'Замок-фрегат и каньон Ахсинта',
    image: '/vue-tour-osetia/images/digorya.jpg',
    color: '#f687b3'
  },
  {
    id: 6,
    category: 'gorges',
    title: 'Кармадонское ущелье',
    description: 'Термальные источники и минеральные воды',
    longDescription: 'Кармадонское ущелье — одно из самых живописных мест Северной Осетии. Здесь расположены минеральные источники, живописные скалы и чистые родники. Маршрут подходит для однодневных и многодневных прогулок, с возможностью отдыха у термальных источников и фотостопов у ключевых видов.',
    image: '/vue-tour-osetia/images/karmadon.jpeg',
    photos: [
      '/vue-tour-osetia/images/karmadon.jpeg',
      '/vue-tour-osetia/images/fiagdon.jpg',
      '/vue-tour-osetia/images/ceiskoe.jpg'
    ],
    color: '#38b2ac'
  },
  {
    id: 7,
    category: 'culture',
    title: 'Даргавское ущелье',
    description: 'Город мертвых и Мидаграбинские водопады',
    image: '/vue-tour-osetia/images/dargavs.jpg',
    color: '#9f7aea'
  },
  {
    id: 8,
    category: 'culture',
    title: 'Меч в камне',
    description: 'Легендарный арт-объект Осетии',
    image: '/vue-tour-osetia/images/mech.webp',
    color: '#e53e3e'
  }
]

const filteredImages = ref(images)

const filterImages = (category) => {
  activeCategory.value = category
  if (category === 'all') {
    filteredImages.value = images
  } else {
    filteredImages.value = images.filter(img => img.category === category)
  }
}

const currentPhotoIndex = ref(0)

const openImage = (image) => {
  selectedImage.value = image
  currentPhotoIndex.value = 0
}

const closeImage = () => {
  selectedImage.value = null
}

const selectedPhoto = computed(() => {
  if (!selectedImage.value) return ''
  if (selectedImage.value.photos && selectedImage.value.photos.length) {
    return selectedImage.value.photos[currentPhotoIndex.value]
  }
  return selectedImage.value.image
})

const nextPhoto = () => {
  if (!selectedImage.value || !selectedImage.value.photos) return
  currentPhotoIndex.value = (currentPhotoIndex.value + 1) % selectedImage.value.photos.length
}

const prevPhoto = () => {
  if (!selectedImage.value || !selectedImage.value.photos) return
  currentPhotoIndex.value = (currentPhotoIndex.value - 1 + selectedImage.value.photos.length) % selectedImage.value.photos.length
}

const goToPhoto = (i) => {
  if (!selectedImage.value || !selectedImage.value.photos) return
  currentPhotoIndex.value = i
}

// Prevent body scroll when modal is open
watch(selectedImage, (val) => {
  if (val) {
    document.documentElement.style.overflow = 'hidden'
    document.body.style.overflow = 'hidden'
  } else {
    document.documentElement.style.overflow = ''
    document.body.style.overflow = ''
  }
})

onBeforeUnmount(() => {
  // cleanup in case component is unmounted while modal is open
  document.documentElement.style.overflow = ''
  document.body.style.overflow = ''
})
</script>

<template>
  <section id="gallery" class="gallery">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Популярные маршруты</h2>
        <p class="section-subtitle">Исследуйте красоту горных ущелий Северной Осетии</p>
      </div>

      <div class="category-filters">
        <button
          v-for="category in categories"
          :key="category.id"
          @click="filterImages(category.id)"
          class="filter-btn"
          :class="{ active: activeCategory === category.id }"
        >
          {{ category.name }}
        </button>
      </div>

      <div class="gallery-grid">
        <div
          v-for="image in filteredImages"
          :key="image.id"
          class="gallery-item"
          @click="openImage(image)"
          :style="{ 
            backgroundImage: `url(${image.image})`,
            backgroundSize: 'cover',
            backgroundPosition: 'center'
          }"
        >
          <div class="gallery-overlay">
            <h3 class="gallery-title">{{ image.title }}</h3>
            <p class="gallery-description">{{ image.description }}</p>
            <div class="view-icon">👁️</div>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal -->
    <transition name="modal">
      <div v-if="selectedImage" class="modal" @click="closeImage">
        <div class="modal-content" @click.stop>
          <button class="close-btn" @click="closeImage">&times;</button>

          <div class="modal-body">
            <div class="modal-gallery">
              <button class="nav-arrow left" @click="prevPhoto">‹</button>
              <div 
                class="modal-main-image"
                :style="{ 
                  backgroundImage: `url(${selectedPhoto})`,
                  backgroundSize: 'cover',
                  backgroundPosition: 'center'
                }"
              ></div>
              <button class="nav-arrow right" @click="nextPhoto">›</button>
            </div>

            <div class="modal-info">
              <h2 class="modal-title">{{ selectedImage.title }}</h2>
              <p class="modal-description">{{ selectedImage.longDescription || selectedImage.description }}</p>

              <div v-if="selectedImage.photos && selectedImage.photos.length" class="modal-thumbs">
                <img
                  v-for="(p, idx) in selectedImage.photos"
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
  </section>
</template>

<style scoped>
.gallery {
  padding: 6rem 0;
  background: white;
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

.category-filters {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
}

.filter-btn {
  padding: 0.75rem 1.5rem;
  border: 2px solid #e2e8f0;
  background: white;
  color: #4a5568;
  border-radius: 50px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.filter-btn:hover {
  border-color: #4299e1;
  color: #4299e1;
}

.filter-btn.active {
  background: linear-gradient(135deg, rgba(44, 82, 130, 0.85) 0%, rgba(66, 153, 225, 0.85) 100%);
  color: white;
  border-color: transparent;
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
}

.gallery-item {
  position: relative;
  height: 350px;
  border-radius: 20px;
  overflow: hidden;
  cursor: pointer;
  transition: all 0.4s ease;
}

.gallery-item:hover {
  transform: translateY(-10px) scale(1.02);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
}

.gallery-overlay {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  background: transparent;
  color: white;
  transition: all 0.4s ease;
}

.gallery-item:hover .gallery-overlay {
  background: rgba(0, 0, 0, 0.1);
}

.gallery-title {
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  text-align: center;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
}

.gallery-description {
  font-size: 1.1rem;
  text-align: center;
  opacity: 0.9;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.5);
}

.view-icon {
  font-size: 2rem;
  margin-top: 1rem;
  opacity: 0;
  transform: scale(0);
  transition: all 0.4s ease;
}

.gallery-item:hover .view-icon {
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

.modal-image {
  height: 500px;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 3rem;
  color: white;
}

/* Modal gallery layout */
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
}

.nav-arrow.left { left: -24px }
.nav-arrow.right { right: -24px }

.modal-info {
  color: #edf2f7;
}

.modal-thumbs {
  display: flex;
  gap: 0.5rem;
  margin-top: 1rem;
}

.modal-thumbs img {
  width: 64px;
  height: 48px;
  object-fit: cover;
  border-radius: 8px;
  cursor: pointer;
  opacity: 0.8;
  border: 2px solid transparent;
}

.modal-thumbs img.active {
  opacity: 1;
  border-color: #4299e1;
}

.modal-title {
  font-size: 3rem;
  font-weight: 800;
  margin-bottom: 1rem;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
}

.modal-description {
  font-size: 1.5rem;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
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

@media (max-width: 768px) {
  .gallery {
    padding: 4rem 0;
  }

  .section-title {
    font-size: 2rem;
  }

  .gallery-grid {
    grid-template-columns: 1fr;
  }

  /* На мобильных: показываем фото сначала, затем описание */
  .modal-body {
    display: block;
  }

  .modal-gallery {
    margin-bottom: 1rem;
  }

  .modal-main-image {
    height: 320px;
    border-radius: 12px;
    background-position: center top;
  }

  .modal-thumbs {
    gap: 0.5rem;
    overflow-x: auto;
    padding-bottom: 0.5rem;
  }

  .nav-arrow {
    display: none; /* стрелки не нужны на узком экране, используем миниатюры и свайп */
  }

  .modal-info {
    margin-top: 0.5rem;
  }

  .modal-title {
    font-size: 1.6rem;
  }

  .modal-description {
    font-size: 1rem;
  }
}
</style>
