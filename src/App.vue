<template>
  <HeaderNav />
  <main>
    <HeroSection />
    <GiftsSection />
    <PixSection />
    <ThanksSection />
  </main>
</template>

<script setup>
import HeaderNav from './components/HeaderNav.vue'
import HeroSection from './components/HeroSection.vue'
import GiftsSection from './components/GiftsSection.vue'
import PixSection from './components/PixSection.vue'
import ThanksSection from './components/ThanksSection.vue'
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&family=Lato:wght@300;400;700&display=swap');

*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Lato', sans-serif;
  background-color: #f8f5ff;
  color: #2e2040;
  overflow-x: hidden;
}

main {
  width: 100%;
}
</style>
