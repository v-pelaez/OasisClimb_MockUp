<template>
  <div id="novedades" class="p-4"></div>
  <div class="container-fluid d-flex flex-column gap-4 py-3">
    <div class="row col-12 bg-primary text-black text-uppercase p-5 recorte-bandera">
      <h3 class="fw-bold fst-italic">Novedades</h3>
    </div>

    <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-4 p-2 px-5">
      <div v-for="(noticia, index) in noticias" :key="index" class="col">
        <div
          class="card h-100 shadow-sm"
          data-bs-toggle="tooltip"
          data-bs-placement="top"
          data-bs-title="Esto es una noticia de ejemplo"
        >
          <img
            :src="noticia.img"
            class="card-img-top noticia-img"
            :alt="noticia.titulo"
          />
          <div class="card-body">
            <h5 class="card-title fw-bold">{{ noticia.titulo }}</h5>
            <p class="card-text text-secondary">
              {{ noticia.texto }}
            </p>
          </div>
          <div class="card-footer bg-white border-top-0">
            <small class="text-muted">Publicado {{ noticia.fecha }}</small>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div aria-label="Page navigation example" class="d-flex justify-content-center mb-4 mt-4">
    <ul
      class="pagination"
      data-bs-toggle="popover"
      data-bs-trigger="hover focus"
      data-bs-title="Acción no disponible"
      data-bs-content="La paginación no está disponible en este prototipo."
    >
      <li class="page-item">
        <a class="page-link bg-light text-dark" href="" aria-label="Previous">
          <span aria-hidden="true">&laquo;</span>
        </a>
      </li>
      <li class="page-item active"><a class="page-link">1</a></li>
      <li class="page-item"><a class="page-link bg-light text-dark" >2</a></li>
      <li class="page-item"><a class="page-link bg-light text-dark" >3</a></li>
      <li class="page-item">
        <a class="page-link bg-light text-dark"  aria-label="Next">
          <span aria-hidden="true">&raquo;</span>
        </a>
      </li>
    </ul>
  </div>
  <div id="ranking"></div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
// Importamos los componentes de Bootstrap necesarios
import { Tooltip, Popover } from 'bootstrap'

// Datos de las noticias para evitar repetir código HTML
const noticias = ref([
  {
    titulo: 'Tradicional en roca: aventuras en la naturaleza',
    texto: 'La escalada tradicional apuesta por la equipación manual y la lectura de la roca, brindando libertad y responsabilidad en cada vía. [...]',
    img: new URL('../assets/thumbnails/climbing-2609319_1280.jpg', import.meta.url).href,
    fecha: 'hace 1 hora'
  },
  {
    titulo: 'Escalada deportiva urbana: superando límites',
    texto: 'Practicada en entornos urbanos, la escalada deportiva combina técnica y destreza, demostrando que cualquier pared puede ser un reto vertical. [...]',
    img: new URL('../assets/thumbnails/free-climbing-4196577_1280.jpg', import.meta.url).href,
    fecha: 'hace 3 horas'
  },
  {
    titulo: 'Rutas en nieve: exploración y resistencia',
    texto: 'Las travesías en nieve invitan a descubrir la montaña de otra forma, combinando orientación, técnica y preparación física. [...]',
    img: new URL('../assets/thumbnails/snow-8033482_1280.jpg', import.meta.url).href,
    fecha: 'hace 1 día'
  },
  {
    titulo: 'Cumbre compartida: logro y compañerismo',
    texto: 'Alcanzar la cima simboliza el esfuerzo colectivo, la superación personal y el disfrute del paisaje en lo más alto. [...]',
    img: new URL('../assets/thumbnails/mountaineer-396533_1280.jpg', import.meta.url).href,
    fecha: 'hace 2 días'
  },
  {
    titulo: 'Montañismo alpino: retos en la altura',
    texto: 'Superar grandes cumbres implica esfuerzo físico y mental, además de trabajo en equipo y buena planificación para alcanzar la cima. [...]',
    img: new URL('../assets/thumbnails/mountain-climbing-1840220_1280.jpg', import.meta.url).href,
    fecha: 'hace 3 días'
  },
  {
    titulo: 'Rutas en nieve: exploración y resistencia',
    texto: 'Las travesías en nieve invitan a descubrir la montaña de otra forma, combinando orientación, técnica y preparación física. [...]',
    img: new URL('../assets/thumbnails/mountain-8488489_1280.jpg', import.meta.url).href,
    fecha: 'hace 3 días'
  }
])

onMounted(() => {
  // Inicializar todos los Tooltips
  const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]')
  tooltipTriggerList.forEach(el => new Tooltip(el))

  // Inicializar todos los Popovers
  const popoverTriggerList = document.querySelectorAll('[data-bs-toggle="popover"]')
  popoverTriggerList.forEach(el => new Popover(el))
})
</script>

<style scoped>
.recorte-bandera {
  clip-path: polygon(0 0, 100% 0, 95% 50%, 100% 100%, 0 100%);
  margin-bottom: 2rem;
}

.noticia-img {
  height: 220px;
  object-fit: cover;
}

.card {
  transition: transform 0.3s ease;
  cursor: pointer;
}

.card:hover {
  transform: translateY(-8px);
}

.pagination {
  cursor: help;
}
</style>