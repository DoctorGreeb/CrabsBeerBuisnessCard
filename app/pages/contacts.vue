<template>
    <ContactsHead />
    <div class="wrapper">
        <div class="main-block">
            <div class="contacts-block">
                <ContactsFeedback />
            </div>
            <div class="map-block">
                <ContactsMap />
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
    min-height: 400px;
    background-color: var(--color-amber-50);
    position: relative;
}

.main-block {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
    gap: 20px;
    width: 1400px;
    padding-top: 3rem;
    padding-bottom: 3rem;
}

.contacts-block, .map-block {
    width: 50%;
    min-height: 800px;
}

</style>