<template>
  <section class="gifts" id="gifts">
    <div class="gifts__header">
      <p class="gifts__eyebrow">Para a nossa nova casinha</p>
      <h2 class="gifts__title">Lista de <em>Presentes</em></h2>
      <div class="gifts__divider">
        <span></span><span class="gifts__leaf">✦</span><span></span>
      </div>
      <p class="gifts__subtitle">
        Cada presente será recebido com muito carinho e amor.
      </p>
    </div>

    <div class="gifts__grid">
      <div
        v-for="gift in gifts"
        :key="gift.id"
        class="gift-card"
        @click="openUrl(gift.url)"
      >
        <div class="gift-card__icon">{{ gift.icon }}</div>
        <h3 class="gift-card__name">{{ gift.name }}</h3>
        <p class="gift-card__desc">{{ gift.desc }}</p>
        <span class="gift-card__link">Ver produto →</span>
        <button
          class="gift-card__btn"
          :class="{ 'gift-card__btn--gifted': giftedIds.has(gift.id) }"
          @click.stop="toggleGifted(gift.id)"
        >
          <span v-if="!giftedIds.has(gift.id)">✅ Disponível</span>
          <span v-else>🎁 Já foi presenteado</span>
        </button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const STORAGE_KEY = 'cha-casa-gifted'
const saved = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]')
const giftedIds = ref(new Set(saved))

function toggleGifted(id) {
  const updated = new Set(giftedIds.value)
  updated.has(id) ? updated.delete(id) : updated.add(id)
  giftedIds.value = updated
  localStorage.setItem(STORAGE_KEY, JSON.stringify([...updated]))
}

function openUrl(url) {
  if (url && url !== '#') window.open(url, '_blank', 'noopener,noreferrer')
}
const gifts = [
  { id: 1,  icon: '', name: 'Varal de Roupas',        desc: 'Varal de chão dobrável', url: 'https://shopee.com.br/Varal-De-Ch%C3%A3o-De-Roupas-3-Andares-Dobr%C3%A1vel-Grande-4-Rodas-i.1243683750.19099664173?extraParams=%7B%22display_model_id%22%3A267068776540%2C%22model_selection_logic%22%3A3%7D&sp_atk=01256ebc-9835-4366-adcc-a181dd38379a&xptdk=01256ebc-9835-4366-adcc-a181dd38379a' },
  { id: 2,  icon: '', name: 'Jogo de Pratos',         desc: '6 pratos rasos',       url: 'https://shopee.com.br/Kit-6-Pratos-Raso-Moderno-100-Porcelana-27-cm-i.1522422029.22098466104?extraParams=%7B%22display_model_id%22%3A219174410525%2C%22model_selection_logic%22%3A3%7D' },
  { id: 3,  icon: '', name: 'Jogo de Talheres',         desc: 'Jogo de talheres 24 peças - Tramontina',       url: 'https://shopee.com.br/Faqueiro-Jogo-de-Talheres-B%C3%BAzios-24-pe%C3%A7as-Faqueiro-Tramontina-A%C3%A7o-Inox-Tramontina-utens%C3%ADlios-cozinha-i.291932836.10363619008?extraParams=%7B%22display_model_id%22%3A143477980120%2C%22model_selection_logic%22%3A3%7D&rModelId=143477980120&sp_atk=9ba1b6a6-3dde-4c18-8a43-a283a6069003&vItemId=58252453202&vModelId=149789145615&vShopId=1665239494&xptdk=9ba1b6a6-3dde-4c18-8a43-a283a6069003' },
  { id: 4,  icon: '', name: 'Escorredor de Louça',         desc: 'Escorredor e organizador de louças',         url: 'https://br.shp.ee/2KNWCxb2' },
  { id: 5,  icon: '', name: 'Jogo de Facas',                desc: 'Jogo de 6 facas tramontina',           url: 'https://br.shp.ee/hehPjfFx' },
  { id: 6,  icon: '', name: 'Kit Mesa Posta',          desc: 'Mesa posta de couro ao estilo americano',      url: 'https://shopee.com.br/Kit-Jogo-Americano-Couro-Redondo-Retangular-Org%C3%A2nico-Mesa-Posta-Jantar-Porta-Copos-Porta-Guardanapo-i.932819770.23497916372?extraParams=%7B%22display_model_id%22%3A129652443247%2C%22model_selection_logic%22%3A3%7D&sp_atk=4e45fbc5-1094-4ee8-9c27-7bbaafda4da0&xptdk=4e45fbc5-1094-4ee8-9c27-7bbaafda4da0' },
  { id: 7,  icon: '🪴', name: 'Plantas Decorativas',     desc: 'Para trazer vida ao lar',          url: '#' },
  { id: 8,  icon: '🛏️', name: 'Jogo de Cama',            desc: 'Lençol casal + fronhas',           url: '#' },
  { id: 9,  icon: '🛁', name: 'Jogo de Toalhas',         desc: 'Toalha de banho e rosto',          url: '#' },
  { id: 10, icon: '🪣', name: 'Kit de Limpeza',          desc: 'Vassoura, rodo e balde',           url: '#' },
  { id: 11, icon: '🧊', name: 'Baldes e Potes',          desc: 'Organizadores para a cozinha',     url: '#' },
  { id: 12, icon: '🥘', name: 'Travessas de Servir',     desc: 'Refratárias e porcelana',          url: '#' },
  { id: 13, icon: '🫙', name: 'Porta-condimentos',       desc: 'Pote de vidro com tampa',          url: '#' },
  { id: 14, icon: '🧴', name: 'Kit Banheiro',            desc: 'Saboneteira, porta-shampoo',       url: '#' },
  { id: 15, icon: '💡', name: 'Luminária Decorativa',    desc: 'Abajur ou luminária de mesa',      url: '#' },
  { id: 16, icon: '🖼️', name: 'Quadros Decorativos',    desc: 'Arte para as paredes',             url: '#' },
  { id: 17, icon: '🪞', name: 'Espelho',                 desc: 'Espelho decorativo de parede',     url: '#' },
  { id: 18, icon: '🧹', name: 'Aspirador',               desc: 'Aspirador portátil',               url: '#' },
  { id: 19, icon: '🍶', name: 'Garrafa Térmica',         desc: 'Para manter bebidas quentes',      url: '#' },
  { id: 20, icon: '🫖', name: 'Chaleira Elétrica',       desc: 'Para o ritual do café da manhã',   url: '#' },
]
</script>

<style scoped>
.gifts {
  background: linear-gradient(180deg, #f0eaff 0%, #f8f5ff 100%);
  padding: 6rem 2rem;
  position: relative;
  overflow: hidden;
}

.gifts::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 3px;
  background: linear-gradient(90deg, transparent, #b08ee0, transparent);
}

/* Header */
.gifts__header {
  text-align: center;
  max-width: 600px;
  margin: 0 auto 4rem;
}

.gifts__eyebrow {
  font-family: 'Lato', sans-serif;
  font-weight: 300;
  font-size: 0.85rem;
  letter-spacing: 0.25rem;
  text-transform: uppercase;
  color: #8b5fc0;
  margin-bottom: 1rem;
}

.gifts__title {
  font-family: 'Cormorant Garamond', serif;
  font-weight: 300;
  font-size: clamp(2.5rem, 5vw, 4rem);
  color: #2e2040;
  margin-bottom: 1.2rem;
}

.gifts__title em {
  font-style: italic;
  color: #7c4daa;
}

.gifts__divider {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  justify-content: center;
  margin-bottom: 1.2rem;
}

.gifts__divider span:not(.gifts__leaf) {
  display: block;
  width: 60px;
  height: 1px;
  background: linear-gradient(90deg, transparent, #b08ee0, transparent);
}

.gifts__leaf {
  color: #b08ee0;
  font-size: 0.75rem;
}

.gifts__subtitle {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.1rem;
  font-style: italic;
  color: #6e5090;
}

/* Grid — 5 colunas */
.gifts__grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 1.2rem;
  max-width: 1280px;
  margin: 0 auto;
}

/* Card */
.gift-card {
  background: rgba(255, 255, 255, 0.80);
  border: 1px solid rgba(176, 142, 224, 0.25);
  border-radius: 14px;
  padding: 1.6rem 1.2rem 1.4rem;
  text-align: center;
  cursor: pointer;
  text-decoration: none;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease, border-color 0.3s ease;
  position: relative;
  overflow: hidden;
}

.gift-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(230,215,255,0.45), transparent);
  opacity: 0;
  transition: opacity 0.3s ease;
  border-radius: inherit;
  pointer-events: none;
}

.gift-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 16px 40px rgba(124, 77, 170, 0.15);
  border-color: rgba(176, 142, 224, 0.55);
}

.gift-card:hover::before {
  opacity: 1;
}

.gift-card__icon {
  font-size: 2.4rem;
  margin-bottom: 0.7rem;
  display: block;
  line-height: 1;
  transition: transform 0.3s ease;
}

.gift-card:hover .gift-card__icon {
  transform: scale(1.15);
}

.gift-card__name {
  font-family: 'Cormorant Garamond', serif;
  font-weight: 500;
  font-size: 1rem;
  color: #2e2040;
  margin-bottom: 0.4rem;
  line-height: 1.3;
}

.gift-card__desc {
  font-family: 'Lato', sans-serif;
  font-size: 0.78rem;
  color: #8870a8;
  font-weight: 300;
  line-height: 1.4;
  margin-bottom: 0.5rem;
}

/* "Ver produto →" aparece no hover */
.gift-card__link {
  font-family: 'Lato', sans-serif;
  font-size: 0.72rem;
  font-weight: 600;
  letter-spacing: 0.08rem;
  color: #8b5fc0;
  opacity: 0;
  transform: translateY(4px);
  transition: opacity 0.3s ease, transform 0.3s ease;
  display: block;
  margin-bottom: 0.7rem;
}

.gift-card:hover .gift-card__link {
  opacity: 1;
  transform: translateY(0);
}

/* Toggle button */
.gift-card__btn {
  margin-top: auto;
  width: 100%;
  padding: 0.42rem 0.5rem;
  border-radius: 8px;
  border: 1.5px solid #5cb85c;
  background: #5cb85c;
  color: #fff;
  font-family: 'Lato', sans-serif;
  font-size: 0.72rem;
  font-weight: 700;
  cursor: pointer;
  transition: background 0.22s ease, border-color 0.22s ease, color 0.22s ease, transform 0.18s ease;
  white-space: nowrap;
}

.gift-card__btn:hover {
  filter: brightness(0.93);
  transform: scale(1.03);
}

/* Gifted state — muted purple outline */
.gift-card__btn--gifted {
  background: transparent;
  border-color: rgba(176, 142, 224, 0.6);
  color: #8b5fc0;
}

.gift-card:hover .gift-card__link {
  opacity: 1;
  transform: translateY(0);
}

/* Responsive */
@media (max-width: 1100px) {
  .gifts__grid { grid-template-columns: repeat(4, 1fr); }
}
@media (max-width: 800px) {
  .gifts__grid { grid-template-columns: repeat(3, 1fr); }
}
@media (max-width: 560px) {
  .gifts__grid { grid-template-columns: repeat(2, 1fr); }
}
</style>
