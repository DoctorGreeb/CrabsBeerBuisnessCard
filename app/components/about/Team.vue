<template>
  <div class="main-wrapper">
    <div class="title">
      <h2>Наши партнёры</h2>
      <h1>Взгляните на их отзывы</h1>
    </div>
    <div class="reviews-grid">
      <div v-for="(video, index) in videos" :key="index" class="video-card">
        <div class="video-wrapper" @click="playVideo(index)">
          <img
            v-if="!video.isPlaying"
            :src="video.poster"
            class="poster"
            alt="Отзыв"
          />
          <video
            :ref="(el) => (videoRefs[index] = el)"
            :src="video.src"
            class="video"
            controls
            playsinline
            preload="none"
            @play="video.isPlaying = true"
          ></video>
          <div v-if="!video.isPlaying" class="play-overlay">
            <div class="play-button">▶</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";

const videoRefs = ref([]);

const videos = reactive([
  {
    src: "https://dl.dropboxusercontent.com/scl/fi/1wapbmm34tr60phrr9wow/stavropol.mp4?rlkey=835uebyh6adtk2vwz63akihq1&st=pifbmk0b&dl=0",
    poster: "/team/rect1.webp",
    isPlaying: false,
  },
  {
    src: "https://dl.dropboxusercontent.com/scl/fi/1ec335jahxbqzfko27pc8/juriy.mp4?rlkey=4vjswdpvlp4nr52x46epbvrwe&st=1mhc9d4n&dl=0",
    poster: "/team/rect2.webp",
    isPlaying: false,
  },
  {
    src: "https://dl.dropboxusercontent.com/scl/fi/crkkhg43uzs24i6k64zo1/ilkin.MP4?rlkey=zzv17ikgywoihhjtnqhexjall&st=90k1sqs0&dl=0",
    poster: "/team/rect3.png",
    isPlaying: false,
  },
]);

const playVideo = (index) => {
  const video = videoRefs.value[index];
  if (video) {
    video.play();
    videos[index].isPlaying = true;
  }
};
</script>

<style scoped>

.title {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items:flex-start;
  width: var(--container-5xl);
  overflow: hidden;
  width: 1350px;
  max-width: 1600px;
  margin: 0 auto;
  padding-top: 3rem;
  padding-bottom: 1rem;
}

.main-wrapper h2 {
  font-size: var(--text-2xl);
  font-weight: var(--font-weight-medium);
  margin-bottom: 1rem;
  color: var(--color-amber-600);
  font-family: var(--font-nunito);
}

.main-wrapper h1 {
  font-size: var(--text-3xl);
  font-weight: var(--font-weight-medium);
  color: var(--color-stone-900);
  font-family: var(--font-nunito);
  margin-bottom: 1rem;
}

.reviews-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 24px;
  padding: 24px;
  width: 1350px;
  max-width: 1600px;
  margin: 0 auto;
  justify-content: center;
  padding: 0 20px;
  padding-bottom: 3rem;
}

.video-wrapper {
  position: relative;
  aspect-ratio: 4 / 5;
  background: #000;
  overflow: hidden;
  border-radius: 16px;
  max-height: 520px;
}

.poster,
.video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.video {
  display: none;
}

.video-card .video {
  display: block;
}

.play-overlay {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, 0.45);
  z-index: 2;
}

.play-button {
  width: 70px;
  height: 70px;
  background: var(--color-amber-500);
  color: black;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 34px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
}
</style>
