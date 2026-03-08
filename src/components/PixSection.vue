<template>
  <section class="pix" id="pix">
    <div class="pix__header">
      <p class="pix__eyebrow">Prefere presentear assim?</p>
      <h2 class="pix__title">Vale Pix <em>de Presente</em></h2>
      <div class="pix__divider">
        <span></span><span class="pix__leaf">✦</span><span></span>
      </div>
      <p class="pix__subtitle">
        Qualquer valor será recebido com muito carinho. 💜
      </p>
    </div>

    <div class="pix__grid">
      <button
        v-for="value in values"
        :key="value"
        class="pix__card"
        :class="{ 'pix__card--selected': selected === value }"
        @click="openPix(value)"
      >
        <span class="pix__card-label">R$</span>
        <span class="pix__card-value">{{ value }}</span>
      </button>
    </div>

    <!-- PIX Modal -->
    <Transition name="modal">
      <div v-if="modal.open" class="modal-overlay" @click.self="closeModal">
        <div class="modal">
          <div class="modal__icon">💜</div>
          <p class="modal__title">Contribuição de <strong>R$ {{ modal.value }}</strong></p>
          <p class="modal__desc">Use a chave PIX abaixo para enviar:</p>

          <div class="modal__pix-box">
            <span class="modal__pix-key">{{ pixKey }}</span>
            <button class="modal__copy-btn" @click="copyKey">
              {{ copied ? '✓ Copiado!' : 'Copiar' }}
            </button>
          </div>

          <p class="modal__thanks">Agradecemos de coração! 🌸</p>
          <button class="modal__close" @click="closeModal">Fechar</button>
        </div>
      </div>
    </Transition>
  </section>
</template>

<script setup>
import { ref, reactive } from 'vue'

const pixKey = '06685772581' // ← Substitua pela chave PIX real

const values = [30, 50, 75, 100, 150, 200, 250, 300, 400, 500]
const selected = ref(null)
const copied = ref(false)
const modal = reactive({ open: false, value: null })

function openPix(value) {
  selected.value = value
  modal.value = value
  modal.open = true
  copied.value = false
}

function closeModal() {
  modal.open = false
  selected.value = null
}

async function copyKey() {
  try {
    await navigator.clipboard.writeText(pixKey)
    copied.value = true
    setTimeout(() => { copied.value = false }, 2500)
  } catch {
    copied.value = false
  }
}
</script>

<style scoped>
.pix {
  background: #f8f5ff;
  padding: 5rem 2rem 6rem;
  position: relative;
  overflow: hidden;
}

.pix::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 3px;
  background: linear-gradient(90deg, transparent, #b08ee0, transparent);
}

/* Header */
.pix__header {
  text-align: center;
  max-width: 560px;
  margin: 0 auto 3rem;
}

.pix__eyebrow {
  font-family: 'Lato', sans-serif;
  font-weight: 300;
  font-size: 0.85rem;
  letter-spacing: 0.25rem;
  text-transform: uppercase;
  color: #8b5fc0;
  margin-bottom: 0.8rem;
}

.pix__title {
  font-family: 'Cormorant Garamond', serif;
  font-weight: 300;
  font-size: clamp(2rem, 4vw, 3.2rem);
  color: #2e2040;
  margin-bottom: 1rem;
}

.pix__title em {
  font-style: italic;
  color: #7c4daa;
}

.pix__divider {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  justify-content: center;
  margin-bottom: 1rem;
}

.pix__divider span:not(.pix__leaf) {
  display: block;
  width: 60px;
  height: 1px;
  background: linear-gradient(90deg, transparent, #b08ee0, transparent);
}

.pix__leaf {
  color: #b08ee0;
  font-size: 0.75rem;
}

.pix__subtitle {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.05rem;
  font-style: italic;
  color: #6e5090;
}

/* Value grid */
.pix__grid {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
  max-width: 700px;
  margin: 0 auto;
}

.pix__card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 120px;
  height: 90px;
  background: rgba(255,255,255,0.85);
  border: 1.5px solid rgba(176,142,224,0.3);
  border-radius: 16px;
  cursor: pointer;
  transition: transform 0.25s ease, box-shadow 0.25s ease, border-color 0.25s ease, background 0.25s ease;
  box-shadow: 0 2px 12px rgba(124,77,170,0.06);
}

.pix__card:hover {
  transform: translateY(-5px);
  box-shadow: 0 12px 30px rgba(124,77,170,0.15);
  border-color: rgba(176,142,224,0.6);
}

.pix__card--selected {
  background: #7c4daa;
  border-color: #7c4daa;
}

.pix__card-label {
  font-family: 'Lato', sans-serif;
  font-size: 0.7rem;
  font-weight: 600;
  color: #8b5fc0;
  letter-spacing: 0.05rem;
  transition: color 0.2s;
}

.pix__card--selected .pix__card-label {
  color: rgba(255,255,255,0.75);
}

.pix__card-value {
  font-family: 'Cormorant Garamond', serif;
  font-size: 2rem;
  font-weight: 500;
  color: #2e2040;
  line-height: 1.1;
  transition: color 0.2s;
}

.pix__card--selected .pix__card-value {
  color: #fff;
}

/* ---- Modal ---- */
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(46,32,64,0.55);
  backdrop-filter: blur(4px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal {
  background: #fff;
  border-radius: 20px;
  padding: 2.2rem 2rem 1.8rem;
  width: min(400px, 92vw);
  box-shadow: 0 24px 60px rgba(124,77,170,0.25);
  text-align: center;
}

.modal__icon {
  font-size: 2.5rem;
  margin-bottom: 0.6rem;
}

.modal__title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.5rem;
  color: #2e2040;
  margin-bottom: 0.3rem;
}

.modal__desc {
  font-family: 'Lato', sans-serif;
  font-size: 0.88rem;
  color: #8870a8;
  margin-bottom: 1.2rem;
}

/* PIX key box */
.modal__pix-box {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  background: #f0eaff;
  border: 1.5px solid rgba(176,142,224,0.4);
  border-radius: 12px;
  padding: 0.7rem 1rem;
  margin-bottom: 1.2rem;
}

.modal__pix-key {
  flex: 1;
  font-family: 'Lato', sans-serif;
  font-size: 0.95rem;
  font-weight: 600;
  color: #5a3d80;
  text-align: left;
  word-break: break-all;
}

.modal__copy-btn {
  background: #7c4daa;
  color: #fff;
  border: none;
  border-radius: 8px;
  padding: 0.4rem 0.85rem;
  font-family: 'Lato', sans-serif;
  font-size: 0.78rem;
  font-weight: 700;
  cursor: pointer;
  white-space: nowrap;
  transition: filter 0.2s;
}

.modal__copy-btn:hover {
  filter: brightness(0.9);
}

.modal__thanks {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.05rem;
  font-style: italic;
  color: #8870a8;
  margin-bottom: 1.4rem;
}

.modal__close {
  background: #f0eaff;
  color: #7c4daa;
  border: none;
  border-radius: 10px;
  padding: 0.55rem 2rem;
  font-family: 'Lato', sans-serif;
  font-size: 0.85rem;
  font-weight: 700;
  cursor: pointer;
  transition: filter 0.2s;
}

.modal__close:hover {
  filter: brightness(0.95);
}

/* Transition */
.modal-enter-active, .modal-leave-active { transition: opacity 0.25s ease; }
.modal-enter-active .modal, .modal-leave-active .modal { transition: transform 0.25s ease; }
.modal-enter-from, .modal-leave-to { opacity: 0; }
.modal-enter-from .modal, .modal-leave-to .modal { transform: scale(0.92); }
</style>
