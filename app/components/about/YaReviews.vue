<template>
  <div class="wrapper">
    <div class="title">
      <h2>Наши довольные клиенты</h2>
      <h1>Посмотрите и оцените</h1>
    </div>
    <div
      style="width: 560px; height: 800px; overflow: hidden; position: relative"
    >
      <iframe
        style="
          width: 100%;
          height: 100%;
          border: 1px solid #e6e6e6;
          border-radius: 8px;
          box-sizing: border-box;
        "
        src="https://yandex.ru/maps-reviews-widget/170773002162?comments"
      >
      </iframe>
      <a
        href="https://yandex.ru/maps/org/krabsbier/170773002162/"
        target="_blank"
        style="
          box-sizing: border-box;
          text-decoration: none;
          color: #b3b3b3;
          font-size: 10px;
          font-family:
            YS Text,
            sans-serif;
          padding: 0 20px;
          position: absolute;
          bottom: 8px;
          width: 100%;
          text-align: center;
          left: 0;
        "
      >
        Krabsbier на карте Ростова-на-Дону — Яндекс Карты
      </a>
    </div>
  </div>
</template>

<script lang="ts"></script>

<style scoped>
html,
body {
  height: 100%;
  margin: 0;
  padding: 0;
}

.wrapper {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10rem;
  margin-bottom: 3rem;
}

.title {
  position: relative;
  height: stretch;
  width: 580px;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  border-radius: 12px;
  overflow: hidden;
  background-color: var(--color-amber-100);
}

.title::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: url("/icons_about/marks1.png");
  background-size: 60px 60px;
  background-repeat: space;
  background-position: center;
  filter: brightness(1.8) saturate(5.8) hue-rotate(2deg) contrast(0.8)
    sepia(0.5);
  z-index: 0;
  pointer-events: none; /* Чтобы не мешать кликам */
}

.title > * {
  position: relative;
  z-index: 1;
}

.title h2 {
  font-size: var(--text-2xl);
  font-weight: var(--font-weight-medium);
  margin-bottom: 1rem;
  color: var(--color-amber-600);
  font-family: var(--font-nunito);
}

.title h1 {
  font-size: var(--text-3xl);
  font-weight: var(--font-weight-medium);
  color: var(--color-stone-900);
  font-family: var(--font-nunito);
  margin-bottom: 1rem;
}

@media (max-width: 1360px) {
  .wrapper {
    gap: 2rem;
  }
}

@media (max-width: 1200px) {
  .wrapper {
    width: auto;
    margin-left: 1rem;
    margin-right: 1rem;
  }
}

@media (max-width: 768px) {
  .wrapper {
    margin-top: 2rem;
    gap: 1rem;
    flex-direction: column;
  }
}
</style>
