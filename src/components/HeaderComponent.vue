<template>
  <header class="container-fluid bg-dark sticky-top">
    <nav class="navbar navbar-expand-lg navbar-dark">
      <a class="navbar-brand" href="#">
        <svg width="100" height="60" fill="#f8c52d" xmlns="http://www.w3.org/2000/svg">
          <use href="../assets/OasisClimb.svg#oasisclimb"></use>
        </svg>
      </a>

      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li v-for="link in navLinks" :key="link.text" class="nav-item">
            <a
              :class="['nav-link', { active: activeSection === link.href.replace('#', '') }]"
              :href="link.href"
              @click="activeSection = link.href.replace('#', '')"
            >
              {{ link.text }}
            </a>
          </li>
        </ul>

        <form class="nav-item d-none d-md-flex flex-nowrap" @submit.prevent role="search">
          <input
            v-model="searchQuery"
            class="form-control me-2"
            type="search"
            placeholder="Buscar..."
            aria-label="Buscar"
          />
          <CPopover
            title="Acción no disponible"
            content="La búsqueda no está disponible en este prototipo."
            placement="left"
            :trigger="['hover', 'focus']"
          >
            <template #toggler="{ id, on }">
              <button v-on="on" :aria-describedby="id" type="button" class="btn btn-primary">
                <CIcon :icon="cilSearch" />
              </button>
            </template>
          </CPopover>
        </form>
      </div>
    </nav>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { CPopover } from '@coreui/vue'
import { CIcon } from '@coreui/icons-vue'
import { cilSearch } from '@coreui/icons'

// 1. Estado para el buscador y la sección activa
const searchQuery = ref('')
const activeSection = ref('novedades') // Por defecto la primera
const popoverBtn = ref(null)

const navLinks = [
  { text: 'Novedades', href: '#novedades' },
  { text: 'Ranking', href: '#ranking' },
  { text: 'Registra tus marcas', href: '#registro' },
  { text: 'Sobre Nosotros', href: '#about-us' },
]

// 3. Lógica de ScrollSpy (Intersection Observer)
let observer = null

onMounted(() => {
  // Inicialización de Popover de Bootstrap
  if (window.bootstrap && popoverBtn.value) {
    new window.bootstrap.Popover(popoverBtn.value)
  }

  // Configuración del observador
  const observerOptions = {
    root: null,
    rootMargin: '-20% 0px -70% 0px', // Margen para detectar la sección en la parte superior
    threshold: 0,
  }

  observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      // Si la sección entra en el "foco" de la pantalla
      if (entry.isIntersecting) {
        activeSection.value = entry.target.id
      }
    })
  }, observerOptions)

  // Decimos al observador que vigile cada ID que definimos en los links
  navLinks.forEach((link) => {
    const id = link.href.replace('#', '')
    const element = document.getElementById(id)
    if (element) observer.observe(element)
  })
})

onUnmounted(() => {
  // Limpieza para evitar fugas de memoria
  if (observer) observer.disconnect()
})
</script>

<style scoped>
/* Estilos específicos */
.navbar-brand svg {
  transition: transform 0.3s ease;
}
.navbar-brand:hover svg {
  transform: scale(1.05);
}

.nav-link.active {
  color: #f0f0f0 !important;
}
</style>
