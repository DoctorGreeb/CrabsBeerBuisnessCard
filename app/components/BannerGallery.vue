<template>
  <section class="gallery-section">
    <div class="gallery-container">

      <div class="gallery-header">
        <span class="gallery-label">Галерея</span>
        <h2 class="gallery-title">Наслаждайтесь видами</h2>
        <p class="gallery-subtitle">
          Визуальное путешествие по нашим магазинам и продукции
        </p>
      </div>

      <div class="gallery-grid">
        <div 
          v-for="(image, index) in images" 
          :key="index"
          class="gallery-card"
        >
          <img 
            :src="image.src" 
            :alt="image.alt"
            class="gallery-image"
          >
          
          <!-- Hover overlay -->
          <div class="gallery-overlay">
            <div class="gallery-overlay-content">
              <p>{{ image.title }}</p>
            </div>
          </div>
        </div>
      </div>

      <div class="gallery-button-wrapper">
        <NuxtLink to="/gallery">
            <button class="gallery-button">
              Смотреть всю галерею
            </button>
        </NuxtLink>
      </div>
    </div>
  </section>
</template>

<script setup>
const images = [
  { 
    src: "/gallery/shop.webp",
    alt: "Интерьер магазина", 
    title: "Интерьер магазина" 
  },
  { 
    src: "/gallery/craft.webp",
    alt: "Крафтовые напитки",
    title: "Крафтовые напитки"
  },
  { 
    src: "/gallery/dryed_fish.webp",
    alt: "Прилавок", 
    title: "Прилавок сухих закусок" 
  },
  { 
    src: "/gallery/nuts.webp",
    alt: "Ассортимент", 
    title: "Ассортимент" 
  },
  { 
    src: "/gallery/showcases.webp",
    alt: "Витрины", 
    title: "Витрины" 
  },
  { 
    src: "/gallery/crayfishes.webp",
    alt: "Живые раки", 
    title: "Живые раки"
  }
]
</script>

<style scoped>
.gallery-section {
  padding: 5rem 0;
  background: linear-gradient(to bottom right, var(--color-amber-950), var(--color-stone-900), var(--color-amber-900));
  color: var(--color-white);
}

.gallery-container {
  max-width: var(--container-7xl);
  margin: 0 auto;
  padding: 0 1.5rem;
}

.gallery-header {
  text-align: center;
  margin-bottom: 4rem;
}

.gallery-label {
  color: var(--color-amber-400);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  font-size: var(--text-sm);
  font-weight: var(--font-weight-medium);
  font-family: var(--font-nunito);
}

.gallery-title {
  font-size: var(--text-5xl);
  font-family: var(--font-rubik);
  font-weight: var(--font-weight-normal);
  margin: 0.75rem 0 1rem 0;
}

.gallery-subtitle {
  color: var(--color-amber-200);
  font-family: var(--font-nunito);
  max-width: 42rem;
  margin: 0 auto;
  font-size: var(--text-lg);
  opacity: 0.85;
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 1.5rem;
  width: 1350px;
  max-width: 1600px;
  margin: 0 auto;
}

.gallery-card {
  position: relative;
  overflow: hidden;
  border-radius: 1.5rem;
  aspect-ratio: 1 / 1;
  cursor: pointer;
}

.gallery-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.7s ease;
}

.gallery-card:hover .gallery-image {
  transform: scale(1.12);
}

.gallery-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to top, rgba(0,0,0,0.85), rgba(0,0,0,0.3), transparent);
  opacity: 0;
  transition: opacity 0.4s ease;
  display: flex;
  align-items: flex-end;
}

.gallery-card:hover .gallery-overlay {
  opacity: 1;
}

.gallery-overlay-content {
  padding: 1.75rem;
  color: var(--color-amber-100);
}

.gallery-overlay-content svg {
  margin-bottom: 0.75rem;
  color: var(--color-amber-400);
}

.gallery-overlay-content p {
  font-weight: var(--font-weight-medium);
  font-size: var(--text-base);
}

.gallery-button-wrapper {
  text-align: center;
  margin-top: 3.5rem;
}

.gallery-button {
  background: linear-gradient(to right, var(--color-amber-500), var(--color-orange-500));
  color: var(--color-white);
  padding: 1rem 2.5rem;
  border-radius: 9999px;
  font-size: var(--text-lg);
  font-weight: var(--font-weight-semibold);
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
  transition: all 0.3s ease;
  border: none;
  cursor: pointer;
}

.gallery-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 20px 40px rgba(245, 158, 11, 0.3);
}
</style>