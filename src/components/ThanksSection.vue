<template>
  <section class="thanks" id="thanks">
    <div class="thanks__bg-decoration" aria-hidden="true">
      <span v-for="i in 8" :key="i" class="thanks__bubble" :style="bubbleStyle(i)"></span>
    </div>

    <div class="thanks__content">

      <p class="thanks__eyebrow">Com todo o nosso amor</p>
      <h2 class="thanks__title">Muito <em>Obrigada!</em></h2>

      <div class="thanks__divider">
        <span></span><span>✦</span><span></span>
      </div>

      <p class="thanks__message">
        Ter vocês ao nosso lado nesse momento tão especial<br />
        significa o mundo para nós.<br /><br />
        Cada presente, cada abraço, cada sorriso compartilhado<br />
        vão tornar essa casa ainda mais cheia de amor.<br /><br />
        <strong>Que a nossa nova casa se torne o lar mais acolhedor,</strong><br />
        repleto de alegrias, memórias e pessoas queridas.
      </p>

      <div class="thanks__signature">
        <p>Com carinho,</p>
        <p class="thanks__name">Julia &amp; Noah</p>
      </div>

      <div class="thanks__footer-ornament">
        <span>🌸</span><span>✦</span><span>🌸</span>
      </div>
    </div>
  </section>
</template>

<script setup>
function bubbleStyle(i) {
  const items = [
    { width: '180px', height: '180px', top: '10%',  left: '5%',  opacity: 0.07 },
    { width: '260px', height: '260px', top: '-5%',  left: '75%', opacity: 0.06 },
    { width: '120px', height: '120px', top: '55%',  left: '88%', opacity: 0.08 },
    { width: '200px', height: '200px', top: '70%',  left: '2%',  opacity: 0.07 },
    { width: '90px',  height: '90px',  top: '35%',  left: '10%', opacity: 0.09 },
    { width: '150px', height: '150px', top: '85%',  left: '55%', opacity: 0.06 },
    { width: '100px', height: '100px', top: '20%',  left: '92%', opacity: 0.08 },
    { width: '220px', height: '220px', top: '45%',  left: '45%', opacity: 0.05 },
  ]
  const s = items[(i - 1) % items.length]
  return {
    width:   s.width,
    height:  s.height,
    top:     s.top,
    left:    s.left,
    opacity: s.opacity,
  }
}
</script>

<style scoped>
.thanks {
  position: relative;
  background: linear-gradient(160deg, #2a1a42 0%, #3d2260 50%, #5c3585 100%);
  padding: 7rem 2rem;
  overflow: hidden;
  text-align: center;
}

/* Decorative blobs */
.thanks__bg-decoration {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.thanks__bubble {
  position: absolute;
  border-radius: 50%;
  background: rgba(200, 170, 255, 1);
}

/* Content */
.thanks__content {
  position: relative;
  z-index: 2;
  max-width: 680px;
  margin: 0 auto;
}

/* House icon */
.thanks__icon-wrap {
  margin-bottom: 1.5rem;
}

.thanks__heart {
  font-size: 4rem;
  display: inline-block;
  animation: pulse 2.5s ease-in-out infinite;
  filter: drop-shadow(0 4px 20px rgba(180,130,255,0.45));
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50%       { transform: scale(1.1); }
}

.thanks__eyebrow {
  font-family: 'Lato', sans-serif;
  font-weight: 300;
  font-size: 0.85rem;
  letter-spacing: 0.25rem;
  text-transform: uppercase;
  color: #c9a8ff;
  margin-bottom: 1rem;
}

.thanks__title {
  font-family: 'Cormorant Garamond', serif;
  font-weight: 300;
  font-size: clamp(2.8rem, 6vw, 5rem);
  color: #f5f0ff;
  margin-bottom: 1.4rem;
  line-height: 1.1;
}

.thanks__title em {
  font-style: italic;
  color: #d4aaff;
}

/* Divider */
.thanks__divider {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  justify-content: center;
  margin-bottom: 2.5rem;
}

.thanks__divider span:nth-child(1),
.thanks__divider span:nth-child(3) {
  display: block;
  width: 70px;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(196,160,255,0.7), transparent);
}

.thanks__divider span:nth-child(2) {
  color: #c9a8ff;
  font-size: 0.75rem;
}

/* Message */
.thanks__message {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.2rem;
  line-height: 2;
  color: #ddc8ff;
  font-style: italic;
  margin-bottom: 2.8rem;
}

.thanks__message strong {
  font-style: normal;
  font-weight: 500;
  color: #eedfff;
}

/* Signature */
.thanks__signature {
  margin-bottom: 2.5rem;
}

.thanks__signature p:first-child {
  font-family: 'Lato', sans-serif;
  font-size: 0.85rem;
  letter-spacing: 0.15rem;
  color: #b090d8;
  margin-bottom: 0.4rem;
}

.thanks__name {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.8rem;
  font-style: italic;
  color: #f5f0ff;
}

/* Footer ornament */
.thanks__footer-ornament {
  display: flex;
  gap: 1rem;
  justify-content: center;
  font-size: 1.2rem;
  opacity: 0.65;
  color: #c9a8ff;
}
</style>
