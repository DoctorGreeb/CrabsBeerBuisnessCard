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
          <img :src="item.src" :alt="item.title" class="gallery-image" />

          <div class="card-desc">
            <p class="card-desc-name category-tag">{{ item.title }}</p>
            <p class="card-desc-text">{{ item.description }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- модалка -->
    <div v-if="isModalOpen" class="modal-overlay" @click.self="closeModal">
      <div class="modal-content">
        <button class="modal-close" @click="closeModal">✕</button>

        <div class="modal-body">
          <!-- Фото -->
          <div class="modal-photo">
            <img :src="selectedItem.src" :alt="selectedItem.title" />
          </div>

          <!-- Название и опис -->
          <div class="modal-info">
            <p class="modal-category">{{ selectedItem.category }}</p>
            <h2 class="modal-title">{{ selectedItem.title }}</h2>
            <p class="modal-description">{{ selectedItem.description || 'Описание скоро появится...' }}</p>
          </div>
        </div>

        <!-- Комменты -->
        <div class="comments-section">
          <h3>Комментарии</h3>

          <div class="comments-list">
            <div v-for="(comment, i) in comments" :key="i" class="comment-item">
              <div class="comment-header">
                <strong>{{ comment.author }}</strong>
                <span class="comment-date">{{ comment.date }}</span>
              </div>
              <p class="comment-text">{{ comment.text }}</p>
              <div class="comment-actions">
                <button @click="editComment(i)" class="edit-btn">Редактировать</button>
                <button @click="deleteComment(i)" class="delete-btn">Удалить</button>
              </div>
            </div>
          </div>

          <div class="comment-form">
            <textarea
              v-model="newCommentText"
              placeholder="Напишите ваш комментарий..."
              rows="3"
            ></textarea>
            <button @click="addComment" class="submit-comment-btn">
              Оставить комментарий
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from "vue";

const activeCategory = ref("Всё");
const selectedIndex = ref(null);
const isModalOpen = ref(false);

const categories = ["Всё", "Морепродукты", "Закуски", "Напитки"];

const images = [
  {
    src: "/gallery/sea/raki.webp",
    category: "Морепродукты",
    title: "Раки",
    description:
      "Свежие варёные раки с укропом, ароматными специями и лимоном. Классическая закуска к пиву.",
  },
  {
    src: "/gallery/sea/crowfish.webp",
    category: "Морепродукты",
    title: "Живой рак",
    description:
      "Живой речной рак — гарантия максимальной свежести. Выбирайте своего рака прямо из аквариума.",
  },
  {
    src: "/gallery/sea/crowfish2.webp",
    category: "Морепродукты",
    title: "Аквариум с раками",
    description:
      "Большой аквариум с живыми раками. У нас всегда только свежий улов.",
  },
  {
    src: "/gallery/sea/sea_kit.webp",
    category: "Морепродукты",
    title: "Набор",
    description:
      "Морской сет — идеальный выбор для компании. Включает раков, креветки и другие дары моря.",
  },
  {
    src: "/gallery/sea/shrimp.webp",
    category: "Морепродукты",
    title: "Креветки",
    description:
      "Крупные отварные креветки с нежным мясом. Подаются с соусом на выбор.",
  },
  {
    src: "/gallery/sea/shrimps.webp",
    category: "Морепродукты",
    title: "Букет креветок",
    description:
      "Красивый букет из крупных креветок — эффектная и вкусная подача для ваших гостей.",
  },

  {
    src: "/gallery/apetisers/asdsa.webp",
    category: "Закуски",
    title: "Орешки",
    description:
      "Ассорти солёных орешков: арахис, фисташки, миндаль и кешью. Идеальная закуска к напиткам.",
  },
  {
    src: "/gallery/apetisers/XXXL (1).webp",
    category: "Закуски",
    title: "Сухарики",
    description:
      "Хрустящие ржаные сухарики с чесноком и зеленью. Классика к пиву.",
  },
  {
    src: "/gallery/apetisers/XXXL (2).webp",
    category: "Закуски",
    title: "Крафтовые закуски",
    description:
      "Премиальные крафтовые закуски ручной работы — для настоящих ценителей.",
  },
  {
    src: "/gallery/apetisers/XXXL.webp",
    category: "Закуски",
    title: "Кукурузные чипсы",
    description:
      "Хрустящие кукурузные чипсы с натуральной морской солью. Отлично сочетаются с соусами.",
  },

  {
    src: "/gallery/drinks/med.webp",
    category: "Напитки",
    title: "Медовые напитки",
    description:
      "Натуральные напитки на основе мёда: медовуха, сбитень и авторские вариации.",
  },
  {
    src: "/gallery/drinks/rfdgredg.webp",
    category: "Напитки",
    title: "Холодные напитки",
    description: "Большой выбор освежающих холодных напитков для любой погоды.",
  },
  {
    src: "/gallery/drinks/sidr.webp",
    category: "Напитки",
    title: "Яблочные напитки",
    description:
      "Лёгкие и ароматные яблочные напитки — от классического сидра до свежих соков.",
  },
  {
    src: "/gallery/drinks/XXXL (1).webp",
    category: "Напитки",
    title: "Крафтовый сидр",
    description:
      "Премиальный крафтовый сидр из отборных яблок. Насыщенный вкус и лёгкая кислинка.",
  },
  {
    src: "/gallery/drinks/XXXL (2).webp",
    category: "Напитки",
    title: "Большой объем",
    description: "Большие порции напитков — отличный вариант для компании.",
  },
  {
    src: "/gallery/drinks/XXXL (3).webp",
    category: "Напитки",
    title: "Большой выбор",
    description:
      "Широкий ассортимент напитков — от классики до эксклюзивных позиций.",
  },
  {
    src: "/gallery/drinks/XXXL (4).webp",
    category: "Напитки",
    title: "Разные вкусы",
    description:
      "Яркая палитра вкусов: ягодные, фруктовые, пряные и необычные сочетания.",
  },
  {
    src: "/gallery/drinks/XXXL (5).webp",
    category: "Напитки",
    title: "Необычные напитки",
    description:
      "Авторские и экспериментальные напитки для тех, кто любит яркие вкусы.",
  },
  {
    src: "/gallery/drinks/XXXL (6).webp",
    category: "Напитки",
    title: "Витрина с холодными напитками",
    description:
      "Наша витрина с охлаждёнными напитками — всегда большой выбор и идеальная температура.",
  },
  {
    src: "/gallery/drinks/XXXL (7).webp",
    category: "Напитки",
    title: "Премиум крафт",
    description: "Премиум крафтовые напитки от лучших производителей.",
  },
  {
    src: "/gallery/drinks/XXXL (8).webp",
    category: "Напитки",
    title: "Фруктовые вкусы",
    description: "Сочные фруктовые и ягодные напитки — идеально освежают.",
  },
  {
    src: "/gallery/drinks/XXXL.webp",
    category: "Напитки",
    title: "Эксклюзивные напитки",
    description:
      "Эксклюзивная линейка напитков, которую вы не найдёте больше нигде.",
  },
];

const filteredImages = computed(() => {
  if (activeCategory.value === "Всё") return images;
  return images.filter((img) => img.category === activeCategory.value);
});

const selectedItem = computed(() => {
  if (selectedIndex.value === null) return null;
  return filteredImages.value[selectedIndex.value];
});

// Комментарии
const comments = ref([
  {
    author: "Алексей Смирнов",
    date: "Сегодня",
    text: "Очень вкусные раки! Свежие и хорошо приготовлены."
  }
]);
const newCommentText = ref('');

// ====================== МОДАЛКА ======================
const openModal = (index) => {
  selectedIndex.value = index;
  isModalOpen.value = true;
  document.body.style.overflow = "hidden";
};

const closeModal = () => {
  isModalOpen.value = false;
  newCommentText.value = '';
  document.body.style.overflow = "visible";
};

const addComment = () => {
  if (!newCommentText.value.trim()) return;
  comments.value.unshift({
    author: "Вы",
    date: "Только что",
    text: newCommentText.value.trim()
  });
  newCommentText.value = '';
};

const editComment = (index) => {
  const newText = prompt('Редактировать комментарий:', comments.value[index].text);
  if (newText !== null && newText.trim() !== '') {
    comments.value[index].text = newText.trim();
  }
};

const deleteComment = (index) => {
  if (confirm('Удалить этот комментарий?')) {
    comments.value.splice(index, 1);
  }
};

// Навигация (стрелки + клавиатура)
const prevImage = () => {
  if (selectedIndex.value > 0) selectedIndex.value--;
  else selectedIndex.value = filteredImages.value.length - 1;
};

const nextImage = () => {
  if (selectedIndex.value < filteredImages.value.length - 1)
    selectedIndex.value++;
  else selectedIndex.value = 0;
};

const handleKeydown = (e) => {
  if (!isModalOpen.value) return;
  if (e.key === "ArrowLeft") prevImage();
  if (e.key === "ArrowRight") nextImage();
  if (e.key === "Escape") closeModal();
};

onMounted(() => window.addEventListener("keydown", handleKeydown));
onUnmounted(() => window.removeEventListener("keydown", handleKeydown));
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

/* фильтры */
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
  background: linear-gradient(
    to right,
    var(--color-amber-500),
    var(--color-orange-500)
  );
  color: white;
}

/* Галерея */
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 24px;
  padding-bottom: 2rem;
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
  background: linear-gradient(to top, rgba(0, 0, 0, 0.75), transparent 45%);
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

/* модалка */
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.85);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 20px;
}

.modal-content {
  background: var(--color-white);
  width: 100%;
  max-width: 1100px;
  border-radius: 16px;
  max-height: 98vh;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

.modal-close {
  position: absolute;
  top: 20px;
  right: 24px;
  font-size: 32px;
  background: none;
  border: none;
  color: var(--color-gray-600);
  cursor: pointer;
  z-index: 10;
}

.modal-body {
  display: flex;
  gap: 32px;
  padding: 40px 40px 0;
  flex: 1;
}

.modal-photo {
  flex: 1;
  border-radius: 12px;
  overflow: hidden;
  background: #f5f5f5;
  height: 400px;
}

.modal-photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.modal-info {
  flex: 1;
}

.modal-category {
  color: var(--color-orange-600);
  font-weight: var(--font-weight-semibold);
  margin-bottom: 8px;
}

.modal-title {
  font-size: var(--text-4xl);
  font-weight: var(--font-weight-bold);
  color: var(--color-gray-900);
  margin: 0 0 20px 0;
}

.modal-description {
  font-size: var(--text-lg);
  line-height: 1.65;
  color: var(--color-gray-700);
}

.comments-section {
  padding: 1rem 40px;
  background: var(--color-gray-50);
}

.comments-section h3 {
  margin: 0 0 20px 0;
}

.comments-list {
  max-height: 320px;
  overflow-y: auto;
  margin-bottom: 20px;
}

.comment-item {
  background: var(--color-white);
  padding: 16px;
  border-radius: 10px;
  margin-bottom: 12px;
  border: 1px solid var(--color-gray-200);
}

.comment-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
}

.comment-date {
  color: var(--color-gray-500);
  font-size: var(--text-sm);
}

.comment-actions button {
  margin-right: 8px;
  padding: 5px 12px;
  border-radius: 6px;
  border: none;
  cursor: pointer;
  font-size: 0.9rem;
}

.edit-btn { background: var(--color-amber-100); color: var(--color-amber-700); }
.delete-btn { background: var(--color-red-600); color: white; }

.comment-form textarea {
  width: 100%;
  padding: 14px;
  border: 2px solid var(--color-gray-300);
  border-radius: 10px;
  resize: vertical;
}

.submit-comment-btn {
  margin-top: 8px;
  padding: 12px 28px;
  background: var(--color-orange-600);
  color: white;
  border: none;
  border-radius: 10px;
  font-weight: var(--font-weight-semibold);
  cursor: pointer;
}

@media (max-width: 768px) {
  .modal-body {
    flex-direction: column;
    gap: 24px;
  }
  .modal-photo {
    height: 320px;
  }
}
</style>