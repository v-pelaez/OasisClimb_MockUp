<template>
  <div class="container-fluid bg-custom-yellow text-dark text-center py-3 shadow">
    <h5 class="mb-0 fw-bold">Conoce la pasión que nos mueve.</h5>
  </div>
  <img :src="imgCabecera" class="w-100 overflow-hidden cabecera" alt="Montaña" />

  <div id="about-us" class="min-vh-100 d-flex flex-column justify-content-center align-items-center py-5 bg-dark text-white">
    <div class="container-fluid">
      <div class="row col-12 bg-custom-yellow text-black text-uppercase p-5 recorte-bandera my-1 mb-5">
        <h3 class="fw-bold fst-italic">Sobre Nosotros</h3>
      </div>
    </div>

    <div class="container w-75 bg-dark text-white p-5 rounded-0 col-md-8 shadow-lg border-start border-custom-yellow border-4 mt-4">
      <div class="row g-5 align-items-center">
        <div class="col-lg-6">
          <h4 class="text-custom-yellow fw-bold text-uppercase mb-4">Nuestra Historia y Misión</h4>
          <p class="lead text-justify">
            En un mundo donde la huella humana a menudo desdibuja la naturaleza, nace Oasis Climb con una misión clara: preservar y compartir el legado de la montaña.
          </p>
          <p class="text-justify mb-4 opacity-75">
            Creemos que cada ruta, cada cima, cada vía ferrata, es una historia grabada en el paisaje, un desafío superado y un tesoro a proteger. Nuestro objetivo es crear una comunidad donde el conocimiento técnico y la seguridad sean primordiales.
          </p>
          <p class="small text-custom-yellow fst-italic">"La montaña es un eco de la eternidad."</p>
        </div>

        <div class="col-lg-6">
          <div class="video-frame border border-custom-yellow border-3 shadow-lg rounded-0 overflow-hidden">
            <video 
              controls 
              :poster="videoPoster"
              class="w-100 d-block"
              preload="metadata"
            >
              <source :src="videoUrl" type="video/mp4">
              Tu navegador no soporta la reproducción de videos.
            </video>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Importación de imagen
const imgCabecera = new URL('../assets/rappel.jpg', import.meta.url).href

// IMPORTANTE: Para videos locales en los assets, usamos la misma lógica que con las imágenes
const videoUrl = new URL('../assets/aboutus.webm', import.meta.url).href

const videoPoster = new URL('../assets/videoposter.png', import.meta.url).href
</script>

<style scoped>
/* Color de marca personalizado */
.bg-custom-yellow {
  background-color: #f8c52d !important;
}
.text-custom-yellow {
  color: #f8c52d !important;
}
.border-custom-yellow {
  border-color: #f8c52d !important;
}

.recorte-bandera {
  clip-path: polygon(0 0, 100% 0, 95% 50%, 100% 100%, 0 100%);
}

.cabecera {
  height: 300px;
  object-fit: cover;
  filter: grayscale(40%) brightness(0.8);
}

.text-justify {
  text-align: justify;
}

/* Contenedor de video cuadrado y sólido */
.video-frame {
  background: #000;
  line-height: 0; /* Elimina espacios residuales debajo del video */
}

video:focus {
  outline: none;
}

/* Placeholder color personalizado */
::placeholder {
  color: #adb5bd !important;
  opacity: 1;
}
</style>