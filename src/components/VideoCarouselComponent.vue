<template>
  <div class="header-banner bg-custom-yellow text-dark text-center py-2 shadow-sm">
    <h6 class="mb-0 fw-bold text-uppercase italic">Aspira, construye, logra.</h6>
  </div>

  <div class="hero-wrapper position-relative bg-black overflow-hidden">
    <div class="progress-container">
      <div :key="currentIndex" class="progress-bar-fill"></div>
    </div>

    <div class="slides-container h-100 w-100">
      <transition name="video-crossfade">
        <div :key="currentIndex" class="slide-item">
          <video 
            class="video-bg" 
            autoplay 
            muted 
            loop 
            playsinline
            disablePictureInPicture
          >
            <source :src="videos[currentIndex].src" type="video/webm">
            <source :src="videos[currentIndex].src" type="video/mp4">
          </video>
        </div>
      </transition>

      <div class="overlay-content">
        <transition name="text-anim" mode="out-in">
          <div v-if="showText" :key="currentIndex" class="text-box border-start border-custom-yellow border-5 shadow-lg">
            <h1 class="display-3 fw-black text-custom-yellow text-uppercase mb-1">
              {{ videos[currentIndex].phrase }}
            </h1>
            <p class="fs-4 text-white text-uppercase opacity-75 fw-light italic">
              {{ videos[currentIndex].subtext }}
            </p>
          </div>
        </transition>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted, onUnmounted } from 'vue';

const videos = reactive([
  { 
    src: new URL('../assets/aspira.webm', import.meta.url).href, 
    phrase: "La mirada en lo alto",
    subtext: "Visualiza la línea donde otros solo ven vacío."
  },
  { 
    src: new URL('../assets/construye.webm', import.meta.url).href, 
    phrase: "El movimiento preciso",
    subtext: "Tu progreso se esculpe paso a paso, agarre a agarre."
  },
  { 
    src: new URL('../assets/logra.webm', import.meta.url).href, 
    phrase: "La cumbre es el camino",
    subtext: "El éxito es la armonía entre tu voluntad y la roca."
  }
]);

const currentIndex = ref(0);
const showText = ref(true);
let cycleTimer = null;

const runCycle = () => {
  // 1. Ocultar texto 1 segundo antes del cambio
  setTimeout(() => {
    showText.value = false;
  }, 5000);

  // 2. Cambiar índice a los 6 segundos
  setTimeout(() => {
    currentIndex.value = (currentIndex.value + 1) % videos.length;
    showText.value = true;
  }, 6000);
};

onMounted(() => {
  cycleTimer = setInterval(runCycle, 6000);
});

onUnmounted(() => {
  clearInterval(cycleTimer);
});
</script>

<style scoped>
/* Colores y Utilidades */
.bg-custom-yellow { background-color: #f8c52d !important; }
.text-custom-yellow { color: #f8c52d !important; }
.border-custom-yellow { border-color: #f8c52d !important; }
.bg-black { background-color: #000 !important; }

.hero-wrapper { height: 90vh; width: 100vw; position: relative; background: #000; }
.slide-item { position: absolute; width: 100%; height: 100%; top: 0; left: 0; background: #000; }
.video-bg { width: 100%; height: 100%; object-fit: cover; }

/* --- TRANSICIÓN DE VIDEO: FUNDIDO A NEGRO --- */
/* Aumentamos el tiempo a 2.5s para que el paso por el negro sea elegante */
.video-crossfade-enter-active,
.video-crossfade-leave-active {
  transition: opacity 2.5s ease-in-out;
}

.video-crossfade-enter-from,
.video-crossfade-leave-to {
  opacity: 0;
}

/* --- ANIMACIÓN DEL TEXTO --- */
.text-anim-enter-active { transition: all 0.8s ease-out; }
.text-anim-leave-active { transition: all 0.5s ease-in; }
.text-anim-enter-from { transform: scale(0.95); opacity: 0; }
.text-anim-leave-to { transform: scale(1.05); opacity: 0; }

.overlay-content {
  position: absolute; top: 0; left: 0; width: 100%; height: 100%;
  display: flex; justify-content: center; align-items: center; z-index: 10;
  pointer-events: none; /* Permite scroll si el ratón está sobre el texto */
}

.text-box {
  background-color: rgba(0, 0, 0, 0.75);
  padding: 2.5rem 4rem;
  backdrop-filter: blur(10px);
  text-align: center;
  pointer-events: auto;
}

/* Barra de progreso */
.progress-container {
  position: absolute; bottom: 0; left: 0; width: 100%; height: 6px;
  background: rgba(255, 255, 255, 0.05); z-index: 50;
}
.progress-bar-fill {
  height: 100%; background-color: #f8c52d; width: 0%;
  animation: progressAnimation 6s linear infinite;
}

@keyframes progressAnimation {
  from { width: 0%; } to { width: 100%; }
}

.fw-black { font-weight: 900; text-shadow: 0 4px 20px rgba(0,0,0,1); }
</style>