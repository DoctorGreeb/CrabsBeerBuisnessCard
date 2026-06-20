<template>
  <div>
    <!-- фильтры -->
    <div class="sticky-filters">
      <div class="gallery-container">
        <div class="filters-wrapper">
          <button 
            v-for="(category, index) in categories"
            :key="index"
            :class="['filter-btn', { active: activeCategory === category }]"
            @click="activeCategory = category"
          >
            {{ category }}
          </button>
        </div>
      </div>
    </div>

    <!-- Галерея -->
    <div class="gallery-container">
      <div class="gallery-grid">
        <div 
          v-for="(item, index) in filteredImages"
          :key="index"
          class="gallery-card"
          @click="openModal(index)"
        >
          <img :src="item.src" :alt="item.title" class="gallery-image">
          
          <div class="card-desc">
            <p class="card-desc-name category-tag">{{ item.title }}</p>
            <p class="card-desc-text">{{ item.description }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Модалка -->
    <div v-if="selectedIndex !== null" class="modal" @click="closeModal">
      <button class="modal-close" @click="closeModal">✕</button>
      
      <button class="nav-btn left" @click.stop="prevImage">←</button>

      <div class="modal-content" @click.stop>
        <img 
          :src="filteredImages[selectedIndex].src" 
          :alt="filteredImages[selectedIndex].title" 
          class="modal-image"
        >
        <div class="modal-info">
          <span class="category-tag category-tag-size">{{ filteredImages[selectedIndex].category }}</span>
          <p class="modal-title">{{ filteredImages[selectedIndex].title }}</p>
        </div>
      </div>

      <button class="nav-btn right" @click.stop="nextImage">→</button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const activeCategory = ref('Всё')
const selectedIndex = ref(null)

const categories = ['Всё', 'Морепродукты', 'Закуски', 'Напитки']

const images = [
  { 
    src: "/gallery/sea/raki.webp", 
    category: "Морепродукты", 
    title: "Раки", 
    description: "Свежие варёные раки с укропом, ароматными специями и лимоном. Классическая закуска к пиву." 
  },
  { 
    src: "/gallery/sea/crowfish.webp", 
    category: "Морепродукты", 
    title: "Живой рак", 
    description: "Живой речной рак — гарантия максимальной свежести. Выбирайте своего рака прямо из аквариума." 
  },
  { 
    src: "/gallery/sea/crowfish2.webp", 
    category: "Морепродукты", 
    title: "Аквариум с раками", 
    description: "Большой аквариум с живыми раками. У нас всегда только свежий улов." 
  },
  { 
    src: "/gallery/sea/sea_kit.webp", 
    category: "Морепродукты", 
    title: "Набор", 
    description: "Морской сет — идеальный выбор для компании. Включает раков, креветки и другие дары моря." 
  },
  { 
    src: "/gallery/sea/shrimp.webp", 
    category: "Морепродукты", 
    title: "Креветки", 
    description: "Крупные отварные креветки с нежным мясом. Подаются с соусом на выбор." 
  },
  { 
    src: "/gallery/sea/shrimps.webp", 
    category: "Морепродукты", 
    title: "Букет креветок", 
    description: "Красивый букет из крупных креветок — эффектная и вкусная подача для ваших гостей." 
  },

  { 
    src: "/gallery/apetisers/asdsa.webp", 
    category: "Закуски", 
    title: "Орешки", 
    description: "Ассорти солёных орешков: арахис, фисташки, миндаль и кешью. Идеальная закуска к напиткам." 
  },
  { 
    src: "/gallery/apetisers/XXXL (1).webp", 
    category: "Закуски", 
    title: "Сухарики", 
    description: "Хрустящие ржаные сухарики с чесноком и зеленью. Классика к пиву." 
  },
  { 
    src: "/gallery/apetisers/XXXL (2).webp", 
    category: "Закуски", 
    title: "Крафтовые закуски", 
    description: "Премиальные крафтовые закуски ручной работы — для настоящих ценителей." 
  },
  { 
    src: "/gallery/apetisers/XXXL.webp", 
    category: "Закуски", 
    title: "Кукурузные чипсы", 
    description: "Хрустящие кукурузные чипсы с натуральной морской солью. Отлично сочетаются с соусами." 
  },

  { 
    src: "/gallery/drinks/med.webp", 
    category: "Напитки", 
    title: "Медовые напитки", 
    description: "Натуральные напитки на основе мёда: медовуха, сбитень и авторские вариации." 
  },
  { 
    src: "/gallery/drinks/rfdgredg.webp", 
    category: "Напитки", 
    title: "Холодные напитки", 
    description: "Большой выбор освежающих холодных напитков для любой погоды." 
  },
  { 
    src: "/gallery/drinks/sidr.webp", 
    category: "Напитки", 
    title: "Яблочные напитки", 
    description: "Лёгкие и ароматные яблочные напитки — от классического сидра до свежих соков." 
  },
  { 
    src: "/gallery/drinks/XXXL (1).webp", 
    category: "Напитки", 
    title: "Крафтовый сидр", 
    description: "Премиальный крафтовый сидр из отборных яблок. Насыщенный вкус и лёгкая кислинка." 
  },
  { 
    src: "/gallery/drinks/XXXL (2).webp", 
    category: "Напитки", 
    title: "Большой объем", 
    description: "Большие порции напитков — отличный вариант для компании." 
  },
  { 
    src: "/gallery/drinks/XXXL (3).webp", 
    category: "Напитки", 
    title: "Большой выбор", 
    description: "Широкий ассортимент напитков — от классики до эксклюзивных позиций." 
  },
  { 
    src: "/gallery/drinks/XXXL (4).webp", 
    category: "Напитки", 
    title: "Разные вкусы", 
    description: "Яркая палитра вкусов: ягодные, фруктовые, пряные и необычные сочетания." 
  },
  { 
    src: "/gallery/drinks/XXXL (5).webp", 
    category: "Напитки", 
    title: "Необычные напитки", 
    description: "Авторские и экспериментальные напитки для тех, кто любит яркие вкусы." 
  },
  { 
    src: "/gallery/drinks/XXXL (6).webp", 
    category: "Напитки", 
    title: "Витрина с холодными напитками", 
    description: "Наша витрина с охлаждёнными напитками — всегда большой выбор и идеальная температура." 
  },
  { 
    src: "/gallery/drinks/XXXL (7).webp", 
    category: "Напитки", 
    title: "Премиум крафт", 
    description: "Премиум крафтовые напитки от лучших производителей." 
  },
  { 
    src: "/gallery/drinks/XXXL (8).webp", 
    category: "Напитки", 
    title: "Фруктовые вкусы", 
    description: "Сочные фруктовые и ягодные напитки — идеально освежают." 
  },
  { 
    src: "/gallery/drinks/XXXL.webp", 
    category: "Напитки", 
    title: "Эксклюзивные напитки", 
    description: "Эксклюзивная линейка напитков, которую вы не найдёте больше нигде." 
  },
]

const filteredImages = computed(() => {
  if (activeCategory.value === 'Всё') return images
  return images.filter(img => img.category === activeCategory.value)
})

const openModal = (index) => {
  selectedIndex.value = index
  document.body.style.overflow = 'hidden'
}

const closeModal = () => {
  selectedIndex.value = null
  document.body.style.overflow = 'visible'
}

const prevImage = () => {
  if (selectedIndex.value > 0) selectedIndex.value--
  else selectedIndex.value = filteredImages.value.length - 1
}

const nextImage = () => {
  if (selectedIndex.value < filteredImages.value.length - 1) selectedIndex.value++
  else selectedIndex.value = 0
}

const handleKeydown = (e) => {
  if (selectedIndex.value === null) return
  if (e.key === 'ArrowLeft') prevImage()
  if (e.key === 'ArrowRight') nextImage()
  if (e.key === 'Escape') closeModal()
}

onMounted(() => window.addEventListener('keydown', handleKeydown))
onUnmounted(() => window.removeEventListener('keydown', handleKeydown))
</script>

<style scoped>

.card-desc {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  min-height: 120px;
  max-height: 140px;
  padding: 10px;
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(10px);
  color: white;
  font-size: var(--text-sm);
  text-align: left;
}

.card-desc-name {
  font-size: var(--text-lg);
}

.card-desc-text {
  font-size: var(--text-sm);
  font-weight: var(--font-weight-light);
  font-family: var(--font-nunito);
  word-break: break-word;
  text-align: justify;
}

.gallery-container {
  max-width: 1600px;
  width: 1350px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Sticky фильтры */
.sticky-filters {
  position: sticky;
  top: 0px;
  z-index: 40;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(8px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  margin-bottom: 2rem;
}

.filters-wrapper {
  display: flex;
  gap: 12px;
  padding: 20px 0;
  overflow-x: auto;
}

.filter-btn {
  padding: 10px 22px;
  border-radius: 9999px;
  font-size: var(--text-sm);
  white-space: nowrap;
  background: var(--color-amber-100);
  color: var(--color-amber-800);
  border: none;
  cursor: pointer;
  transition: all 0.3s;
}

.filter-btn:hover {
  background: var(--color-amber-200);
}

.filter-btn.active {
  background: linear-gradient(to right, var(--color-amber-500), var(--color-orange-500));
  color: white;
}

/* Галерея */
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 24px;
}

.gallery-card {
  position: relative;
  overflow: hidden;
  border-radius: 16px;
  aspect-ratio: 1 / 1;
  cursor: pointer;
  background: var(--color-amber-100);
}

.gallery-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.7s ease;
}

.gallery-card:hover .gallery-image {
  transform: scale(1.1);
}

.gallery-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to top, rgba(0,0,0,0.75), transparent 45%);
  opacity: 0;
  transition: opacity 0.4s;
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  padding: 24px;
}

.gallery-card:hover .gallery-overlay {
  opacity: 1;
}

.gallery-overlay-content {
  color: white;
}

.category-tag {
  text-transform: uppercase;
  letter-spacing: 1px;
  color: var(--color-amber-300);
  font-weight: var(--font-weight-medium);
  font-family: var(--font-rubik);
}

.category-tag-size {
    font-size: var(--text-xl);
}

.title {
  font-size: var(--text-base);
  font-weight: var(--font-weight-semibold);
  margin-top: 4px;
}

.zoom-icon {
  color: white;
  font-size: 14px;
  align-self: flex-start;
  opacity: 0.9;
}

/* Modal */
.modal {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.93);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 20px;
}

.modal-content {
  position: relative;
  max-width: 95%;
  max-height: 90vh;
}

.modal-image {
  max-width: 100%;
  max-height: 85vh;
  border-radius: 16px;
  box-shadow: 0 30px 70px -15px rgb(0 0 0 / 0.8);
}

.modal-info {
  text-align: center;
  margin-top: 20px;
  color: white;
}

.modal-title {
  font-size: var(--text-xl);
  font-weight: var(--font-weight-semibold);
  margin-top: 8px;
  font-family: var(--font-nunito);
}

.modal-close {
  position: absolute;
  top: -55px;
  right: 10px;
  background: none;
  border: none;
  color: white;
  font-size: 36px;
  cursor: pointer;
  z-index: 1010;
}

.nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0,0,0,0.7);
  color: white;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 30px;
  border: none;
  cursor: pointer;
  z-index: 1010;
  transition: all 0.2s;
}

.nav-btn:hover {
  background: var(--color-amber-500);
  transform: translateY(-50%) scale(1.1);
}

.left  { left: 20px; }
.right { right: 20px; }
</style>