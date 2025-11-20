<script setup>
import Preloader from './components/Preloader.vue'
import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import Services from './components/Services.vue'
import Gallery from './components/Gallery.vue'
import Transport from './components/Transport.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <Preloader />
  <div class="app">
    <Header />
    <Hero />
    <Services />
    <Gallery />
    <Transport />
    <Contact />
    <Footer />
  </div>
</template>
