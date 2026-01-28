<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

// Estado para controlar la visibilidad de la flecha
const isVisible = ref(false);

// Función para mostrar/ocultar el botón según el scroll
const handleScroll = () => {
  isVisible.value = window.scrollY > 300; // Aparece tras bajar 300px
};

// Función para subir con suavidad
const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth' // Desplazamiento fluido
  });
};

onMounted(() => window.addEventListener('scroll', handleScroll));
onUnmounted(() => window.removeEventListener('scroll', handleScroll));
</script>

<template>
  <Transition name="fade">
    <button v-if="isVisible" @click="scrollToTop" class="scroll-top-btn" aria-label="Volver arriba">
      <!-- Icono de flecha simple -->
      <span class="arrow">↑</span>
    </button>
  </Transition>
</template>

<style scoped>
.scroll-top-btn {
  position: fixed;
  bottom: 30px;
  right: 30px;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: #f8c52d; 
  color: white;
  border: none;
  cursor: pointer;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
  z-index: 1000;
  transition: transform 0.2s ease;
}

.scroll-top-btn:hover {
  transform: scale(1.1);
  background-color: #35495e;
}

/* Animación de aparición (Fade) */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>
