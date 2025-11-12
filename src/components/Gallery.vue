<script setup>
import { ref } from 'vue'

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
    category: 'mountains',
    title: 'Цейское ущелье',
    description: 'Величественные горные пейзажи',
    image: '/vue-tour-osetia/images/ceiskoe.jpg',
    color: '#4299e1'
  },
  {
    id: 2,
    category: 'gorges',
    title: 'Кармадонское ущелье',
    description: 'Живописные виды и водопады',
    image: '/vue-tour-osetia/images/karmadon.jpeg',
    color: '#48bb78'
  },
  {
    id: 3,
    category: 'mountains',
    title: 'Дигорское ущелье',
    description: 'Древние башни и природа',
    image: '/vue-tour-osetia/images/digorya.jpg',
    color: '#ed8936'
  },
  {
    id: 4,
    category: 'winter',
    title: 'Зимний Цей',
    description: 'Горнолыжный курорт',
    image: '/vue-tour-osetia/images/ceiskoe.jpg',
    color: '#667eea'
  },
  {
    id: 5,
    category: 'culture',
    title: 'Даргавс - Город мертвых',
    description: 'Древний некрополь',
    image: '/vue-tour-osetia/images/hero3.jpg',
    color: '#f687b3'
  },
  {
    id: 6,
    category: 'gorges',
    title: 'Куртатинское ущелье',
    description: 'Скальные крепости',
    image: '/vue-tour-osetia/images/karmadon.jpeg',
    color: '#38b2ac'
  },
  {
    id: 7,
    category: 'mountains',
    title: 'Казбек',
    description: 'Снежные вершины',
    image: '/vue-tour-osetia/images/hero1.jpg',
    color: '#4299e1'
  },
  {
    id: 8,
    category: 'winter',
    title: 'Снежные пейзажи',
    description: 'Зимняя сказка в горах',
    image: '/vue-tour-osetia/images/hero2.jpg',
    color: '#9f7aea'
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

const openImage = (image) => {
  selectedImage.value = image
}

const closeImage = () => {
  selectedImage.value = null
}
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
            backgroundImage: `linear-gradient(135deg, ${image.color}88 0%, ${image.color}66 100%), url(${image.image})`,
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
          <div 
            class="modal-image"
            :style="{ 
              backgroundImage: `linear-gradient(135deg, ${selectedImage.color}88 0%, ${selectedImage.color}66 100%), url(${selectedImage.image})`,
              backgroundSize: 'cover',
              backgroundPosition: 'center'
            }"
          >
            <h2 class="modal-title">{{ selectedImage.title }}</h2>
            <p class="modal-description">{{ selectedImage.description }}</p>
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
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
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
  background: linear-gradient(135deg, #2c5282 0%, #4299e1 100%);
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
  background: rgba(0, 0, 0, 0.2);
  color: white;
  transition: all 0.4s ease;
}

.gallery-item:hover .gallery-overlay {
  background: rgba(0, 0, 0, 0.6);
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

  .modal-image {
    height: 400px;
  }

  .modal-title {
    font-size: 2rem;
  }

  .modal-description {
    font-size: 1.2rem;
  }
}
</style>
