<template>
  <div class="wrapper">
    <div class="content">
      <div class="blocks">
        <div class="block">
          <div class="logo">
            <NuxtLink to="/">
              <img src="/logo_crabsbeer.svg" alt="logo" />
            </NuxtLink>
          </div>
          <div class="description">
            <p>Добро пожаловать в мир гастрономического удовольствия!</p>
            <p>
              У нас — настоящее изобилие закусок и пенных напитков, которые
              созданы друг для друга.
            </p>
          </div>
        </div>
        <div class="block">
          <div class="title">Ссылки</div>
          <div class="links">
            <NuxtLink to="/">Главная</NuxtLink>
            <NuxtLink to="/about">О нас</NuxtLink>
            <NuxtLink to="/contacts">Контакты</NuxtLink>
            <NuxtLink to="/gallery">Галерея</NuxtLink>
            <NuxtLink to="/assortment">Ассортимент</NuxtLink>
          </div>
        </div>
        <div class="block">
          <div class="title">Контакты</div>
          <div class="contacts">
            <p>+7 (989) 501-85-85</p>
            <p>+7 (904) 501-86-86</p>
            <div class="address">
              <NuxtLink to="https://yandex.ru/maps/-/CPxqAC5D">
                Берберовская ул., 8, стр. 1, Ростов-на-Дону
              </NuxtLink>
            </div>
          </div>
        </div>
        <div class="block">
          <div class="title">Мы есть на картах:</div>
          <div class="social">
            <NuxtLink to="https://yandex.ru/maps/-/CPxqAC5D"
              ><img src="/Yandex_icon.png" alt="Yandex"
            /></NuxtLink>
          </div>
          <div class="description">
            <p>Часы работы</p>
            <p>Пн-Пт: 10:00-23:00</p>
          </div>
        </div>
      </div>
      <div class="copyright">
        <hr />
        <p>© 2026 КрабсБир. Designed by DoctorGreeb</p>
      </div>
    </div>
  </div>
</template>

<script setup></script>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  width: 100%;
  height: 360px;
  background-color: var(--color-amber-950);
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
}

.blocks {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.block {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  width: 100%;
  max-width: var(--container-lg);
  width: var(--container-lg);
  max-height: 260px;
  height: 260px;
  padding-left: 1rem;
  padding-right: 1rem;
}

.links {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: stretch;
  gap: 1rem;
  flex: 1;
}

.description {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  gap: 2rem;
  flex: 1;
}

.links a {
  color: var(--color-amber-100);
  text-decoration: none;
  font-size: var(--text-base);
  font-family: var(--font-sans);
  cursor: pointer;
}

.address a {
  color: var(--color-amber-100);
  text-decoration: none;
  font-size: var(--text-base);
  font-family: var(--font-sans);
  cursor: pointer;
}

.address {
  color: var(--color-amber-100);
  text-decoration: none;
  font-size: var(--text-base);
  font-family: var(--font-sans);
  cursor: pointer;
}

.links a:hover {
  color: var(--color-amber-300);
  text-underline-offset: 2px;
  text-decoration-thickness: 2px;
}

.contacts {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  gap: 2rem;
  flex: 1;
}

p {
  font-size: var(--text-sm);
  font-family: var(--font-nunito);
  color: var(--color-amber-100);
}

img {
  width: 200px;
  height: 100px;
}

.social {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding-top: 2.5rem;
}

.social img {
  width: 50px;
  height: 50px;
}

.title {
  font-size: var(--text-2xl);
  font-family: var(--font-rubik);
  color: var(--color-amber-100);
  font-weight: var(--font-weight-normal);
  padding-top: 2rem;
}

hr {
  border: 1px solid var(--color-amber-900);
  margin-bottom: 2rem;
}

.copyright {
  font-size: var(--text-sm);
  font-family: var(--font-nunito);
  color: var(--color-amber-100);
  padding-top: 2rem;
  width: 100%;
  text-align: center;
  padding-top: 2rem;
  padding-bottom: 2rem;
}

/* Адаптив */
@media (max-width: 1024px) {
  .blocks {
    gap: 2rem;
  }
}

@media (max-width: 768px) {
  .wrapper {
    height: auto;
    padding: 2rem 0;
  }
  
  .blocks {
    flex-direction: column;
    align-items: flex-start;
    gap: 2.5rem;
  }
  
  .block {
    width: 100%;
    max-width: 100%;
    height: auto;
    max-height: none;
    padding: 0 1rem;
  }
  
  .social {
    justify-content: flex-start;
  }
  
  img {
    width: 160px;
    height: auto;
  }
}
</style>
