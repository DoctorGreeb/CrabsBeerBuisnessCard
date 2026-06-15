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
                    <NuxtLink to="/contact">Контакты</NuxtLink>
                </div>
                <div class="button">
                    <NuxtLink to="/menu">Ассортимент</NuxtLink>
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
    background-color: var(--color-amber-900);
}

.content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    max-width: var(--container-7xl);
}


.logo {
    display: flex;
    align-items: center;
    margin-left: 4rem;
    scale: 2;
}

.logo img {
    width: 100px;
    height: 100px;
}

.buttons {
    display: flex;
    align-items: center;
}

.link {
    margin-right: 1rem;
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
    padding: 0.7rem;
}

.button a {
    color: var(--color-amber-100);
    text-decoration: none;
    font-size: var(--text-xl);
    font-family: var(--font-sans);
}
</style>