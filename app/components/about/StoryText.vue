<template>
  <div class="wrapper">
    <div class="content">
      <div class="content-text">
        <div class="title">
          <h2>Наша фишка</h2>
          <h1>
            Производим уникальные снеки и закуски, которые невозможно найти у
            конкурентов
          </h1>
        </div>
        <div class="description">
          <p>
            Оснастили кухню электростатической коптильней и вялочным шкафом.
            Коптим креветки, кальмары, барабульку и другие деликатесы — быстро,
            с сохранением вкуса и аромата. В вялочном шкафу готовим мясные чипсы
            из курицы, индейки, говядины, а также вяленую рыбу
          </p>
          <p>
            Такая кухня превращает наш магазин в гастрономический центр —
            клиенты приходят не только за пивом, но и за интересной, необычной
            закуской
          </p>
        </div>
      </div>
      <div class="image">
        <img src="/banners/snack.webp" alt="snack" />
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
  width: var(--container-5xl);
  overflow: hidden;
  background-color: var(--color-amber-50);
}

.content {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  gap: 2rem;
  width: 70%;
  padding: 3rem;
}

.content-text {
  width: 100%;
  min-width: 300px;
  max-width: 1000px;
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

.description p {
  font-size: var(--text-base);
  font-family: var(--font-nunito);
  color: var(--color-gray-600);
  font-weight: var(--font-weight-medium);
  display: flex;
  margin-bottom: 1rem;
}

.image {
  display: flex;
  justify-content: center;
  align-items: center;
  min-width: 400px;
}

.image img {
  width: 100%;
  border-radius: 1rem;
}
</style>
