<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const currentSlide = ref(0)
const slides = [
  {
    title: 'Горы Северной Осетии',
    subtitle: 'Откройте для себя величие Кавказских гор',
    image: '/vue-tour-osetia/images/hero1.jpg',
    gradient: 'linear-gradient(135deg, rgba(44, 82, 130, 0.7) 0%, rgba(66, 153, 225, 0.6) 100%)'
  },
  {
    title: 'Комфортные перевозки',
    subtitle: 'Toyota Alphard для вашего комфорта',
    image: '/vue-tour-osetia/images/hero2.jpg',
    gradient: 'linear-gradient(135deg, rgba(72, 187, 120, 0.7) 0%, rgba(56, 161, 105, 0.6) 100%)'
  },
  {
    title: 'Профессиональные гиды',
    subtitle: 'Узнайте историю и культуру Осетии',
    image: '/vue-tour-osetia/images/hero3.jpg',
    gradient: 'linear-gradient(135deg, rgba(237, 137, 54, 0.7) 0%, rgba(221, 107, 32, 0.6) 100%)'
  }
]

let interval

onMounted(() => {
  interval = setInterval(() => {
    currentSlide.value = (currentSlide.value + 1) % slides.length
  }, 5000)
})

onUnmounted(() => {
  clearInterval(interval)
})

const setSlide = (index) => {
  currentSlide.value = index
}

const scrollToContact = () => {
  document.getElementById('contact')?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <section id="hero" class="hero">
    <div class="hero-slider">
      <div 
        v-for="(slide, index) in slides" 
        :key="index"
        class="slide"
        :class="{ active: currentSlide === index }"
        :style="{ 
          backgroundImage: `${slide.gradient}, url(${slide.image})`,
          backgroundSize: 'cover',
          backgroundPosition: 'center'
        }"
      >
        <div class="container">
          <div class="hero-content">
            <h1 class="hero-title" data-aos="fade-up">{{ slide.title }}</h1>
            <p class="hero-subtitle" data-aos="fade-up" data-aos-delay="100">{{ slide.subtitle }}</p>
            <div class="hero-buttons" data-aos="fade-up" data-aos-delay="200">
              <button @click="scrollToContact" class="btn btn-primary">Забронировать тур</button>
              <a href="tel:+79999999999" class="btn btn-secondary">Позвонить</a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="slider-dots">
      <button 
        v-for="(slide, index) in slides" 
        :key="index"
        @click="setSlide(index)"
        class="dot"
        :class="{ active: currentSlide === index }"
      ></button>
    </div>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  height: 100vh;
  min-height: 600px;
  overflow: hidden;
  margin-top: 70px;
}

.hero-slider {
  position: relative;
  width: 100%;
  height: 100%;
}

.slide {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 1s ease-in-out;
}

.slide.active {
  opacity: 1;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  width: 100%;
}

.hero-content {
  text-align: center;
  color: white;
  max-width: 800px;
  margin: 0 auto;
}

.hero-title {
  font-size: 4rem;
  font-weight: 800;
  margin-bottom: 1.5rem;
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  animation: fadeInUp 1s ease;
}

.hero-subtitle {
  font-size: 1.5rem;
  margin-bottom: 2.5rem;
  opacity: 0.95;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
  animation: fadeInUp 1s ease 0.2s backwards;
}

.hero-buttons {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  flex-wrap: wrap;
  animation: fadeInUp 1s ease 0.4s backwards;
}

.btn {
  padding: 1rem 2.5rem;
  font-size: 1.1rem;
  font-weight: 600;
  border-radius: 50px;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
  text-decoration: none;
  display: inline-block;
}

.btn-primary {
  background: white;
  color: #2c5282;
  box-shadow: 0 4px 20px rgba(255, 255, 255, 0.3);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 30px rgba(255, 255, 255, 0.4);
}

.btn-secondary {
  background: transparent;
  color: white;
  border: 2px solid white;
}

.btn-secondary:hover {
  background: white;
  color: #2c5282;
  transform: translateY(-3px);
}

.slider-dots {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 1rem;
  z-index: 10;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.5);
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
}

.dot.active {
  background: white;
  width: 40px;
  border-radius: 6px;
}

.scroll-indicator {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  color: white;
  animation: bounce 2s infinite;
}

.mouse {
  width: 30px;
  height: 50px;
  border: 2px solid white;
  border-radius: 15px;
  display: flex;
  justify-content: center;
  padding-top: 8px;
}

.wheel {
  width: 4px;
  height: 10px;
  background: white;
  border-radius: 2px;
  animation: scroll 1.5s infinite;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateX(-50%) translateY(0);
  }
  40% {
    transform: translateX(-50%) translateY(-10px);
  }
  60% {
    transform: translateX(-50%) translateY(-5px);
  }
}

@keyframes scroll {
  0% {
    opacity: 1;
    transform: translateY(0);
  }
  100% {
    opacity: 0;
    transform: translateY(20px);
  }
}

@media (max-width: 768px) {
  .hero-title {
    font-size: 2.5rem;
  }

  .hero-subtitle {
    font-size: 1.2rem;
  }

  .btn {
    padding: 0.875rem 2rem;
    font-size: 1rem;
  }

  .hero-buttons {
    flex-direction: column;
    gap: 1rem;
  }
}
</style>
