<script setup>
import { ref } from 'vue'

const videoLoaded = ref(false)

const scrollToContact = () => {
  document.getElementById('contact')?.scrollIntoView({ behavior: 'smooth' })
}

const onVideoLoaded = () => {
  videoLoaded.value = true
}
</script>

<template>
  <section id="hero" class="hero">
    <!-- Video Background -->
    <div class="video-background">
      <video
        :class="{ 'video-loaded': videoLoaded }"
        autoplay
        muted
        loop
        playsinline
        preload="metadata"
        @loadeddata="onVideoLoaded"
      >
        <source src="/videos/video.mp4" type="video/mp4">
      </video>
      <!-- Fallback image while video loads -->
      <div 
        v-if="!videoLoaded"
        class="video-fallback"
        :style="{ backgroundImage: 'url(/images/hero1.jpg)' }"
      ></div>
    </div>

    <div class="container">
      <div class="hero-content">
        <h1 class="hero-title" data-aos="fade-up">Откройте для себя горы Осетии</h1>
        <p class="hero-subtitle" data-aos="fade-up" data-aos-delay="100">Незабываемые туры по самым живописным местам Кавказа</p>
        <div class="hero-buttons" data-aos="fade-up" data-aos-delay="200">
          <button @click="scrollToContact" class="btn btn-primary">Забронировать тур</button>
          <a href="tel:+79999999999" class="btn btn-secondary">Позвонить</a>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  height: 100vh;
  min-height: 600px;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Video Background Styles */
.video-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.video-background video {
  position: absolute;
  top: 50%;
  left: 50%;
  min-width: 100%;
  min-height: 100%;
  width: auto;
  height: auto;
  transform: translateX(-50%) translateY(-50%);
  object-fit: cover;
  opacity: 0;
  transition: opacity 0.5s ease-in;
}

.video-background video.video-loaded {
  opacity: 1;
}

.video-fallback {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  width: 100%;
  position: relative;
  z-index: 2;
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
  text-shadow: 0 4px 20px rgba(0, 0, 0, 0.8), 0 2px 10px rgba(0, 0, 0, 0.6);
  animation: fadeInUp 1s ease;
}

.hero-subtitle {
  font-size: 1.5rem;
  margin-bottom: 2.5rem;
  opacity: 0.95;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.8), 0 1px 5px rgba(0, 0, 0, 0.6);
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
  
  /* On mobile, reduce video quality impact */
  .video-background video {
    min-width: 100%;
    width: 100%;
  }
}
</style>
