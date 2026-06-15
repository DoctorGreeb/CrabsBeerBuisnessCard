<template>
  <div class="wrapper">
    <div class="content">
      <div class="title">
        <h1>КрабсБир</h1>
      </div>
      <div class="topic">
        <h2>Крафт и закуски</h2>
      </div>
      <div class="description">
        <p>Добро пожаловать в мир гастрономического удовольствия!</p>
        <p>
          У нас — настоящее изобилие закусок и пенных напитков, которые созданы
          друг для друга.
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
  height: 100vh;
  background-color: var(--color-amber-600);
  position: relative;
}

.wrapper::before {
  content: "";
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  background-image: url("/banners/crayfish.webp");
  background-size: cover;
  background-position: center;
  z-index: 1;
  transform: scale(1.001);
  filter: brightness(0.55) saturate(1.4) hue-rotate(12deg) contrast(1.05);
}

.content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 2rem;
  margin-bottom: 2rem;
  max-width: var(--container-7xl);
  min-width: var(--container-md);
  padding: 1rem;
  z-index: 2;
}

.title h1 {
  font-size: var(--text-7xl);
  font-family: var(--font-rubik);
  color: var(--color-amber-100);
  padding-top: 2rem;
  letter-spacing: 1.2rem;
  font-weight: var(--font-weight-medium);
}

.topic h2 {
  font-size: var(--text-5xl);
  font-family: var(--font-rubik);
  color: var(--color-amber-100);
  font-weight: var(--font-weight-medium);
  padding-top: 2rem;
  padding-bottom: 2rem;
  letter-spacing: 0.15rem;
  color: var(--color-amber-300);
}

.description p {
  font-size: var(--text-lg);
  font-family: var(--font-nunito);
  color: var(--color-amber-100);
  width: 100%;
  text-align: center;
  font-weight: var(--font-weight-medium);
}
</style>
