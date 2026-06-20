<template>
  <div class="map-container">
    <h2 class="map-title">Посетите нас</h2>
    <ClientOnly>
      <div ref="mapRef" class="map"></div>
    </ClientOnly>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'

const mapRef = ref(null)
let map = null
let L = null

onMounted(async () => {
  await nextTick()

  if (!mapRef.value) return

  try {

    await import('leaflet/dist/leaflet.css')

    L = (await import('leaflet')).default

    delete L.Icon.Default.prototype._getIconUrl
    L.Icon.Default.mergeOptions({
      iconRetinaUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/images/marker-icon-2x.png',
      iconUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/images/marker-icon.png',
      shadowUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/images/marker-shadow.png',
    })

    map = L.map(mapRef.value, {
      zoomControl: true,
      scrollWheelZoom: true,
    }).setView([47.243043, 39.803046], 16)

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '',
      maxZoom: 19,
      detectRetina: true,
    }).addTo(map)

    const marker = L.marker([47.243043, 39.803046]).addTo(map)

    marker.bindPopup(`
  <div>
    <b  style="font-family: var(--font-rubik); font-size: var(--text-xl);">Crabs & Beer</b><br>
    <div style="font-family: var(--font-nunito); font-size: var(--text-sm);">
        <p>Ростов-на-Дону</p>
        <a href="https://yandex.ru/maps/-/CPxqAC5D" target="_blank">
          Открыть в Яндекс.Картах →
        </a>
    </div>
  </div>
`).openPopup()

    const fixMap = () => {
      if (map) {
        map.invalidateSize()
        setTimeout(() => map.invalidateSize(), 150)
        setTimeout(() => map.invalidateSize(), 400)
        setTimeout(() => map.invalidateSize(), 800)
      }
    }

    fixMap()
    window.addEventListener('resize', fixMap)

  } catch (e) {
    console.error('Ошибка инициализации карты:', e)
  }
})

onBeforeUnmount(() => {
  if (map) map.remove()
})
</script>

<style scoped>
.map-container {
  width: 100%;
}

.map-title {
  text-align: center;
  font-size: var(--text-3xl);
  font-weight: var(--font-weight-normal);
  margin-bottom: 8px;
  color: var(--color-gray-900);
  font-family: var(--font-rubik);
}

.map {
  width: 100%;
  height:760px;
  border-radius: 16px;
  border: 1px solid #ddd;
}


@media (max-width: 768px) {
  .map {
    height: 380px !important;
  }
}
</style>