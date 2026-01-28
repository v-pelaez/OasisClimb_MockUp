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
              :class="['nav-link', { active: link.active }]"
              :aria-current="link.active ? 'page' : null"
              :href="link.href"
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
import { ref, onMounted } from 'vue'
import { CPopover } from '@coreui/vue'
import { CIcon } from '@coreui/icons-vue'
import { cilSearch } from '@coreui/icons'
// Estado para el buscador
const searchQuery = ref('')

// Configuración de los links de navegación
const navLinks = [
  { text: 'Novedades', href: '#novedades', active: true },
  { text: 'Ranking', href: '#ranking', active: false },
  { text: 'Registra tus marcas', href: '#registro', active: false },
  {text: 'Sobre Nosotros', href:'#about-us', active: false}
]

// Inicialización de Bootstrap (Popovers)
const popoverBtn = ref(null)

onMounted(() => {
  // Asegúrate de que Bootstrap esté disponible globalmente o impórtalo
  if (window.bootstrap) {
    new window.bootstrap.Popover(popoverBtn.value)
  }
})
</script>

<style scoped>
/* Estilos específicos si los necesitas, 
   aunque la mayoría vienen de Bootstrap */
.navbar-brand svg {
  transition: transform 0.3s ease;
}
.navbar-brand:hover svg {
  transform: scale(1.05);
}
</style>