<script setup>
const popularRoutes = [
  {
    id: 1,
    title: 'Золотое кольцо',
    description: 'Легендарный маршрут по главным достопримечательностям',
    video: '/videos/cards_videos/koleso.mp4',
    image: '/images/fiagdon.jpg'
  },
  {
    id: 2,
    title: 'Алагирское ущелье',
    description: 'Святилище Уастырджи и источники Тамиск',
    image: '/images/ozero.jpg'
  },
  {
    id: 3,
    title: 'Цейское ущелье',
    description: 'Горнолыжный курорт и ледники',
    image: '/images/ceiskoe.jpg'
  },
  {
    id: 4,
    title: 'Куртатинское ущелье',
    description: 'Каньон Кадаргаван и древние башни',
    image: '/images/kurtatinskoe.jpg'
  },
  {
    id: 5,
    title: 'Дигорское ущелье',
    description: 'Замок-фрегат и каньон Ахсинта',
    image: '/images/digorya.jpg'
  },
  {
    id: 6,
    title: 'Даргавское ущелье',
    description: 'Город мертвых и Мидаграбинские водопады',
    image: '/images/dargavs.jpg'
  }
]
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
          </div>
        </div>
      </div>
    </div>
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

@media (max-width: 968px) {
  .routes-grid {
    grid-template-columns: repeat(2, 1fr);
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
}
</style>
