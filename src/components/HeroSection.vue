<template>
  <section class="hero" id="hero">
    <div class="hero__petals">
      <span v-for="i in 14" :key="i" class="petal" :style="petalStyle(i)">🌸</span>
    </div>

    <div class="hero__content">
      <p class="hero__eyebrow">Você está convidado(a) para o</p>
      <h1 class="hero__title">Chá de<br /><em>Casa Nova</em></h1>
      <div class="hero__divider">
        <span></span><span class="hero__leaf">✦</span><span></span>
      </div>

      <p class="hero__hosts">de Julia &amp; Noah</p>

      <div class="hero__details">
        <div class="hero__detail-item">
          <span class="hero__detail-icon">📅</span>
          <div>
            <strong>Data</strong>
            <p>Sábado, 28 de Março de 2026</p>
          </div>
        </div>
        <div class="hero__detail-sep"></div>
        <div class="hero__detail-item">
          <span class="hero__detail-icon">⏰</span>
          <div>
            <strong>Horário</strong>
            <p>16h00 — até a alegria durar</p>
          </div>
        </div>
        <div class="hero__detail-sep"></div>
        <div class="hero__detail-item">
          <span class="hero__detail-icon">📍</span>
          <div>
            <strong>Endereço</strong>
            <p>Alameda Praia de Caravelas, Quadra D Lote 19<br />Condomínio Porto dos Coqueiros - Stella Maris</p>
          </div>
        </div>
      </div>

      <p class="hero__message">
        Venha celebrar esse momento tão especial conosco!<br />
        A porta estará sempre aberta para quem queremos por perto.
      </p>
    </div>
  </section>
</template>

<script setup>
function petalStyle(i) {
  const positions = [
    { top: '5%',  left: '3%',  size: '1.8rem', delay: '0s',   rot: '-20deg' },
    { top: '12%', left: '90%', size: '2.2rem', delay: '0.4s', rot: '15deg'  },
    { top: '25%', left: '96%', size: '1.5rem', delay: '0.8s', rot: '35deg'  },
    { top: '55%', left: '95%', size: '2rem',   delay: '1.2s', rot: '-10deg' },
    { top: '80%', left: '92%', size: '1.6rem', delay: '0.2s', rot: '25deg'  },
    { top: '88%', left: '6%',  size: '2rem',   delay: '0.6s', rot: '-30deg' },
    { top: '70%', left: '2%',  size: '1.4rem', delay: '1s',   rot: '10deg'  },
    { top: '40%', left: '1%',  size: '1.8rem', delay: '0.3s', rot: '-45deg' },
    { top: '2%',  left: '20%', size: '1.3rem', delay: '0.9s', rot: '50deg'  },
    { top: '3%',  left: '75%', size: '1.6rem', delay: '0.15s',rot: '-15deg' },
    { top: '92%', left: '30%', size: '1.5rem', delay: '0.7s', rot: '20deg'  },
    { top: '93%', left: '60%', size: '2rem',   delay: '0.5s', rot: '-35deg' },
    { top: '18%', left: '5%',  size: '1.3rem', delay: '1.1s', rot: '40deg'  },
    { top: '48%', left: '97%', size: '1.5rem', delay: '0.35s',rot: '-25deg' },
  ]
  const p = positions[(i - 1) % positions.length]
  return {
    top: p.top,
    left: p.left,
    fontSize: p.size,
    animationDelay: p.delay,
    transform: `rotate(${p.rot})`,
  }
}
</script>

<style scoped>
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(160deg, #f8f5ff 0%, #f0eaff 40%, #e8deff 100%);
  padding: 6rem 2rem;
  overflow: hidden;
}

/* Decorative background glow */
.hero::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image:
    radial-gradient(ellipse 120px 120px at 10% 15%, rgba(180,130,240,0.12) 0%, transparent 70%),
    radial-gradient(ellipse 160px 160px at 90% 80%, rgba(160,110,220,0.10) 0%, transparent 70%);
  pointer-events: none;
}

/* Floating petals */
.hero__petals {
  position: absolute;
  inset: 0;
  pointer-events: none;
  overflow: hidden;
}

.petal {
  position: absolute;
  opacity: 0.4;
  animation: floatPetal 6s ease-in-out infinite alternate;
  user-select: none;
}

@keyframes floatPetal {
  0%   { transform: translateY(0)   rotate(-20deg); opacity: 0.3; }
  100% { transform: translateY(-14px) rotate(10deg);  opacity: 0.6; }
}

/* Content */
.hero__content {
  position: relative;
  z-index: 2;
  text-align: center;
  max-width: 680px;
}

.hero__eyebrow {
  font-family: 'Lato', sans-serif;
  font-weight: 300;
  font-size: 0.9rem;
  letter-spacing: 0.25rem;
  text-transform: uppercase;
  color: #8b5fc0;
  margin-bottom: 1.2rem;
}

.hero__title {
  font-family: 'Cormorant Garamond', serif;
  font-weight: 300;
  font-size: clamp(3.5rem, 8vw, 6.5rem);
  line-height: 1.05;
  color: #2e2040;
  margin-bottom: 1.4rem;
}

.hero__title em {
  font-style: italic;
  color: #7c4daa;
}

.hero__divider {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  justify-content: center;
  margin-bottom: 1rem;
}

.hero__divider span:not(.hero__leaf) {
  display: block;
  width: 70px;
  height: 1px;
  background: linear-gradient(90deg, transparent, #b08ee0, transparent);
}

.hero__leaf {
  color: #b08ee0;
  font-size: 0.75rem;
}

.hero__hosts {
  font-family: 'Cormorant Garamond', serif;
  font-style: italic;
  font-size: 1.4rem;
  color: #7c4daa;
  margin-bottom: 2.8rem;
}

/* Details Card */
.hero__details {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  gap: 0;
  background: rgba(255,255,255,0.70);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(176,142,224,0.35);
  border-radius: 16px;
  padding: 2rem 2.5rem;
  box-shadow: 0 8px 32px rgba(124,77,170,0.12), 0 2px 8px rgba(124,77,170,0.06);
  margin-bottom: 2.5rem;
  flex-wrap: wrap;
  gap: 1.5rem;
}

.hero__detail-item {
  display: flex;
  align-items: flex-start;
  gap: 0.8rem;
  text-align: left;
  flex: 1;
  min-width: 160px;
}

.hero__detail-icon {
  font-size: 1.5rem;
  margin-top: 2px;
}

.hero__detail-item strong {
  display: block;
  font-family: 'Lato', sans-serif;
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.2rem;
  text-transform: uppercase;
  color: #8b5fc0;
  margin-bottom: 4px;
}

.hero__detail-item p {
  font-family: 'Lato', sans-serif;
  font-size: 0.9rem;
  color: #3d2e55;
  line-height: 1.5;
}

.hero__detail-sep {
  width: 1px;
  background: rgba(176,142,224,0.45);
  align-self: stretch;
  min-height: 50px;
}

.hero__message {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.15rem;
  line-height: 1.8;
  color: #5e4480;
  font-style: italic;
}
</style>
