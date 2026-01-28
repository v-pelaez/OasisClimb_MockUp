<template>
  <footer class="text-center text-lg-start border border-white  pt-4 bg-dark text-white">
    <div class="container p-4 d-flex justify-content-around">
      <div class="row w-100">
        <div class="col-lg-4 col-md-4 mb-4 mb-lg-0">
          <h5 class="text-uppercase mb-4 fw-bold">Oasis Climb</h5>
          <ul class="list-unstyled mb-4">
            <li v-for="item in menuItems" :key="item.text">
              <a :href="item.link" class="text-white">{{ item.text }}</a>
            </li>
          </ul>
        </div>

        <div class="col-lg-4 col-md-4 mb-4 mb-lg-0 text-white justify-content-start">
          <h5 class="text-uppercase mb-4 fw-bold">Síguenos</h5>
          <div class="d-flex flex-column align-items-center align-items-lg-start justify-content-around gap-1">
            <a v-for="social in socialLinks" :key="social.name" :href="social.url"
              class="text-white d-flex align-items-center" target="_blank" rel="noopener">
              <i :class="[social.icon, 'fa-lg me-2']"></i> {{ social.name }}
            </a>
          </div>
        </div>

        <div class="col-lg-4 col-md-4 mb-4 mb-lg-0">
          <h5 class="text-uppercase mb-4 fw-bold">Suscríbete a nuestro boletín de Novedades</h5>

          <div class="form-outline form-white mb-4">
            <input type="email" v-model="email" class="form-control" placeholder="correo@electronico.com" />
          </div>

          <button ref="subscribeBtn" type="button" class="btn btn-primary text-dark col-12 btn-block mb-4"
            data-bs-toggle="popover" data-bs-title="Acción no disponible"
            data-bs-content="La suscripción no está disponible en este prototipo.">
            Suscríbete
          </button>

          
        </div>
        <div class="d-flex justify-content-center">
            <svg width="200" height="150" viewBox="0 0 200 150" xmlns="http://www.w3.org/2000/svg">
              <path d="M20 110 L60 40 L100 90 L140 30 L180 110 L20 110" fill="none" stroke="#d1d1d1" stroke-width="3"
                stroke-linecap="round" stroke-linejoin="round" />
              <path class="mountain-path-animated" d="M20 110 L60 40 L100 90 L140 30 L180 110 L20 110" fill="none"
                stroke="#f8c52d" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" />
            </svg>
          </div>
      </div>
    </div>

    <div class="text-center p-3 border-top border-white">
      <h5 class="text-uppercase mb-4 fw-bold">Información legal</h5>
      <p class="text-center small px-lg-5">
        Este trabajo ha sido elaborado por V. Peláez con fines académicos. La
        autoría de todo el contenido corresponde exclusivamente a V. Peláez.
        El trabajo no tiene carácter comercial ni busca obtener beneficio
        económico alguno. Las imágenes utilizadas provienen de fuentes como
        Flaticon y Freepik, y se emplean respetando sus licencias de uso
        gratuito y atribución.Queda prohibida la reproducción o distribución
        del contenido para fines comerciales sin el consentimiento explícito
        del autor. Se agradece la adecuada atribución de las imágenes conforme
        a las condiciones de las plataformas.
      </p>
      <a class="text-white" href="https://github.com/v-pelaez" target="_blank">
        <i class="fab fa-github fa-lg me-2"></i>Github
      </a>
    </div>
  </footer>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const email = ref('')
const subscribeBtn = ref(null)

const menuItems = [
  { text: 'Novedades', link: 'index.html#novedades' },
  { text: 'Ranking', link: 'index.html#ranking' },
  { text: 'Registra tus Marcas', link: 'inscripcion.html' },
]

const socialLinks = [
  { name: 'Instagram', url: 'https://www.instagram.com/', icon: 'fab fa-instagram' },
  { name: 'Facebook', url: 'https://www.facebook.com/', icon: 'fab fa-facebook-f' },
  { name: 'Twitter', url: 'https://x.com/', icon: 'fab fa-x-twitter' },
]

onMounted(() => {
  // Inicialización del Popover de Bootstrap
  if (window.bootstrap) {
    new window.bootstrap.Popover(subscribeBtn.value)
  }
})
</script>

<style scoped>
/* Animación del SVG mediante CSS para mayor control en Vue */
.mountain-path-animated {
  stroke-dasharray: 500;
  stroke-dashoffset: 500;
  animation: drawMountain 4s infinite ease-in-out;
}

@keyframes drawMountain {
  0% {
    stroke-dashoffset: 500;
    opacity: 0;
  }

  50% {
    stroke-dashoffset: 0;
    opacity: 1;
  }

  100% {
    stroke-dashoffset: -500;
    opacity: 0;
  }
}

/* Ajuste de estilo para el texto legal */
p {
  font-size: 0.85rem;
  line-height: 1.4;
  max-width: 900px;
  margin: 0 auto 1rem auto;
}
</style>
