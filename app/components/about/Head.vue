<template>
  <div class="wrapper">
    <div class="content">
      <div class="title">
        <h1>Мы - это</h1>
    </div>
      <div class="description">
        <p>
          сеть региональных магазинов разливной продукции и морепродуктов
          премиум-класса.
        </p>
        <p>
          Мы гордимся тем, что предлагаем нашим клиентам только самое лучшее!
        </p>
      </div>
    </div>
  </div>
</template>

<script setup></script>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 400px;
  background-color: var(--color-amber-600);
  position: relative;
}

.wrapper::before {
  content: "";
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  background-image: url("/banners/fish.webp");
  background-size: cover;
  background-position: center;
  z-index: 1;
  transform: scale(1.001);
  filter: brightness(0.55) saturate(5.8) hue-rotate(2deg) contrast(0.75)
    sepia(0.7);
}

.content {
  z-index: 2;
}

.title h1 {
  font-size: var(--text-7xl);
  font-family: var(--font-rubik);
  color: var(--color-amber-100);
  padding-top: 2rem;
  letter-spacing: 1.2rem;
  font-weight: var(--font-weight-medium);
  text-align: center;
  margin-bottom: 1rem;
}

.description p {
  font-size: var(--text-lg);
  font-family: var(--font-nunito);
  color: var(--color-amber-100);
  width: 100%;
  text-align: center;
  font-weight: var(--font-weight-medium);
  margin-bottom: 0.5rem;

}
</style>
