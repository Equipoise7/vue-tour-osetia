<script setup>
import Preloader from './components/Preloader.vue'
import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import ServicesTab from './components/ServicesTab.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <Preloader />
  <div class="app">
    <Header />
    <Hero />
    <ServicesTab />
    <Contact />
    <Footer />
  </div>
</template>
