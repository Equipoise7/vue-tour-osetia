<script setup>
import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import Services from './components/Services.vue'
import Gallery from './components/Gallery.vue'
import Transport from './components/Transport.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
</script>

<template>
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

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  line-height: 1.6;
  color: #333;
  overflow-x: hidden;
}

.app {
  width: 100%;
  overflow-x: hidden;
}
</style>
