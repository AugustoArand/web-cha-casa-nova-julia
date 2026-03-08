<template>
  <header class="nav" :class="{ 'nav--scrolled': scrolled }">
    <div class="nav__brand">
      <span class="nav__icon">🏡</span>
      <span class="nav__title">Chá de Casa Nova</span>
    </div>

    <nav class="nav__links">
      <a href="#gifts" class="nav__link" @click.prevent="scrollTo('gifts')">
         Presentes
      </a>
      <a href="#pix" class="nav__link nav__link--pix" @click.prevent="scrollTo('pix')">
         Vale Pix
      </a>
    </nav>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)

function onScroll() {
  scrolled.value = window.scrollY > 40
}

function scrollTo(id) {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}

onMounted(() => window.addEventListener('scroll', onScroll))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>

<style scoped>
.nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 500;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem 2.5rem;
  transition: background 0.35s ease, box-shadow 0.35s ease, padding 0.3s ease;
}

/* After scrolling — adds frosted glass card */
.nav--scrolled {
  background: rgba(255, 255, 255, 0.82);
  backdrop-filter: blur(14px);
  box-shadow: 0 2px 20px rgba(124, 77, 170, 0.10);
  padding: 0.7rem 2.5rem;
}

/* Brand */
.nav__brand {
  display: flex;
  align-items: center;
  gap: 0.55rem;
  text-decoration: none;
}

.nav__icon {
  font-size: 1.3rem;
  line-height: 1;
}

.nav__title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.1rem;
  font-style: italic;
  color: #3a2e55;
  white-space: nowrap;
}

/* Nav links */
.nav__links {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.nav__link {
  font-family: 'Lato', sans-serif;
  font-size: 0.82rem;
  font-weight: 700;
  text-decoration: none;
  padding: 0.45rem 1.1rem;
  border-radius: 99px;
  letter-spacing: 0.04rem;
  transition: background 0.22s ease, color 0.22s ease, transform 0.2s ease;
  color: #7c4daa;
  background: rgba(176, 142, 224, 0.12);
  border: 1.5px solid rgba(176, 142, 224, 0.3);
}

.nav__link:hover {
  background: rgba(176, 142, 224, 0.22);
  transform: translateY(-1px);
}

/* PIX link — filled */
.nav__link--pix {
  background: #7c4daa;
  color: #fff;
  border-color: #7c4daa;
}

.nav__link--pix:hover {
  background: #6a3d96;
  border-color: #6a3d96;
}

@media (max-width: 480px) {
  .nav {
    padding: 0.8rem 1.2rem;
  }

  .nav--scrolled {
    padding: 0.6rem 1.2rem;
  }

  .nav__title {
    font-size: 0.95rem;
  }

  .nav__link {
    font-size: 0.75rem;
    padding: 0.38rem 0.8rem;
  }
}
</style>
