<template>
    <div class="wrapper">
        <div class="content">
            <div class="logo">
                <NuxtLink to="/">
                    <img src="/logo_crabsbeer.svg" alt="logo">
                </NuxtLink>
            </div>
            <div class="buttons">
                <div class="link">
                    <NuxtLink to="/">Главная</NuxtLink>
                </div>
                <div class="link">
                    <NuxtLink to="/about">О нас</NuxtLink>
                </div>
                <div class="link">
                    <NuxtLink to="/contacts">Контакты</NuxtLink>
                </div>
                <div class="link">
                    <NuxtLink to="/gallery">Галерея</NuxtLink>
                </div>
                <div class="button">
                    <NuxtLink to="/assortment">Ассортимент</NuxtLink>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>


</script>

<style scoped>
.wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 90px;
    background-color: var(--color-amber-800);
}

.content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    max-width: var(--container-7xl);
      min-width: var(--container-md);
    gap: 2rem;
}


.logo {
    display: flex;
    align-items: center;
    margin-left: 4rem;
}

.logo img {
  width: 250px;
}

.buttons {
    display: flex;
    align-items: center;
}

.link {
    margin-right: 1rem;
        min-width: var(--container-xs);
}

.link a {
    color: var(--color-amber-100);
    text-decoration: none;
    font-size: var(--text-xl);
    font-family: var(--font-sans);
}

.link a:hover {
    color: var(--color-amber-300);
    text-decoration: underline;
    text-underline-offset: 8px;
    text-decoration-thickness: 3px;
}

.button {
    margin-left: 1rem;
    margin-right: 1rem;
    background-color: var(--color-orange-500);
    border-radius: 50px;
    padding: 0.9rem;
}

.button a {
    color: var(--color-amber-100);
    text-decoration: none;
    font-size: var(--text-xl);
    font-family: var(--font-sans);
}

/* Адаптив */
@media (max-width: 1024px) {
  .content {
    gap: 1rem;
    padding: 0 1rem;
  }
  .logo img {
    width: 200px;
  }
}

@media (max-width: 860px) {
  .wrapper {
    height: 140px;
  }
  
  .content {
    flex-direction: column;
    gap: 0.75rem;
    padding: 0.5rem;
  }
  
  .logo {
    margin-left: 0;
  }
  
  .logo img {
    width: 180px;
  }
  
  .buttons {
    flex-wrap: wrap;
    justify-content: center;
    gap: 0.5rem;
  }
  
  .link, .button {
    margin: 0;
  }
  
  .link a, .button a {
    font-size: var(--text-base);
  }
}
</style>