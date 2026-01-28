<template>
  <div class="container-fluid bg-primary text-dark-emphasis text-center py-3 shadow">
    <h5 class="mb-0">Haz que tu huella perdure. Registra tu marca, deja tu legado en la roca.</h5>
  </div>
  <img :src="imgCabecera" class="w-100 overflow-hidden cabecera" alt="Montaña" />

  <div id="registro" class="min-vh-100 d-flex flex-wrap justify-content-center align-items-start py-5">
    <div class="container-fluid">
      <div class="row col-12 bg-primary text-black text-uppercase p-5 recorte-bandera my-1 mb-5">
        <h3 class="fw-bold fst-italic">Registra tus marcas</h3>
      </div>
    </div>

    <div class="container w-75 bg-dark text-white p-4 rounded-0 col-md-8 shadow-lg border-start border-primary border-4">
      <form 
        class="row g-3" 
        :class="{ 'was-validated': wasValidated }" 
        @submit.prevent="handleSubmit" 
        novalidate
      >
        <h5 class="col-12 mb-4 text-uppercase fw-bold border-bottom border-primary pb-2">Datos Técnicos de la Ruta</h5>

        <div class="col-md-6">
          <div class="mb-3">
            <label for="routeName" class="form-label">Nombre de la vía o ruta</label>
            <input v-model="formData.routeName" type="text" class="form-control rounded-0" id="routeName" placeholder="Ej: La arista de los vientos" required />
            <div class="invalid-feedback">El nombre es obligatorio.</div>
          </div>

          <div class="mb-3">
            <label for="location" class="form-label">Macizo / Zona / Sector</label>
            <input v-model="formData.location" type="text" class="form-control rounded-0" id="location" placeholder="Ej: Picos de Europa - Naranjo de Bulnes" required />
            <div class="invalid-feedback">Indica la zona geográfica.</div>
          </div>

          <div class="row">
            <div class="col-6 mb-3">
              <label for="markerType" class="form-label">Disciplina</label>
              <select v-model="formData.markerType" class="form-select rounded-0" id="markerType" required>
                <option value="" disabled>Tipo...</option>
                <option value="senderismo">Senderismo</option>
                <option value="ferrata">Vía Ferrata</option>
                <option value="escalada">Escalada</option>
                <option value="alpinismo">Alpinismo</option>
              </select>
            </div>
            <div class="col-6 mb-3">
              <label for="difficulty" class="form-label">Dificultad</label>
              <select v-model="formData.difficulty" class="form-select rounded-0" id="difficulty" required>
                <option value="" disabled>Grado...</option>
                <option value="baja">Baja (K1 / II)</option>
                <option value="media">Media (K3 / V)</option>
                <option value="alta">Alta (K5 / 6b+)</option>
                <option value="extrema">Extrema (K6 / 7+)</option>
              </select>
            </div>
          </div>

          <div class="mb-3">
            <label for="gpsLink" class="form-label">Coordenadas o Enlace Track (GPX)</label>
            <input v-model="formData.gpsLink" type="url" class="form-control rounded-0" id="gpsLink" placeholder="https://wikiloc.com/..." />
          </div>
        </div>

        <div class="col-md-6">
          <div class="row">
            <div class="col-6 mb-3">
              <label for="length" class="form-label">Distancia / Largos</label>
              <input v-model="formData.length" type="text" class="form-control rounded-0" id="length" placeholder="Ej: 12km o 4 largos" required />
            </div>
            <div class="col-6 mb-3">
              <label for="elevation" class="form-label">Desnivel (+m)</label>
              <input v-model="formData.elevation" type="number" class="form-control rounded-0" id="elevation" placeholder="Ej: 850" required />
            </div>
          </div>

          <div class="mb-3">
            <label for="duration" class="form-label">Tiempo estimado (h)</label>
            <input v-model="formData.duration" type="number" class="form-control rounded-0" id="duration" min="0" step="0.5" required />
          </div>

          <div class="mb-3">
            <label for="season" class="form-label">Mejor Época</label>
            <select v-model="formData.season" class="form-select rounded-0" id="season" required>
              <option value="" disabled>Selecciona...</option>
              <option value="primavera">Primavera - Otoño</option>
              <option value="verano">Verano (Alta Montaña)</option>
              <option value="invierno">Invierno (Invernal)</option>
              <option value="todo_el_anyo">Todo el año</option>
            </select>
          </div>

          <div class="mb-3">
            <label for="equipment" class="form-label">Material obligatorio</label>
            <input v-model="formData.equipment" type="text" class="form-control rounded-0" id="equipment" placeholder="Ej: Cuerda 60m, Friends, Casco" required />
          </div>
        </div>

        <div class="col-12 mb-3">
          <label for="description" class="form-label">Descripción del itinerario y marcas</label>
          <textarea v-model="formData.description" class="form-control rounded-0" id="description" rows="3" placeholder="Describe los hitos, marcas de pintura o químicos..." required></textarea>
        </div>

        <div class="col-12 mb-3">
          <div class="form-check">
            <input v-model="formData.terms" type="checkbox" class="form-check-input rounded-0" id="termsCheck" required />
            <label class="form-check-label" for="termsCheck small">Confirmo que la información técnica es veraz y apta para la seguridad de terceros.</label>
          </div>
        </div>

        <div class="col-12 text-end">
          <button class="btn btn-primary px-5 py-2 fw-bold text-uppercase rounded-0" type="submit">
            Registrar Marca
          </button>
        </div>
      </form>
    </div>
  </div>

  <div class="modal fade" id="successModal" tabindex="-1" ref="modalElement" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered">
      <div class="modal-content bg-dark text-white  rounded-0 shadow-lg">
        <div class="modal-header border-bottom  rounded-0">
          <h5 class="modal-title text-primary fw-bold text-uppercase">Envío Completado</h5>
          <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body text-center p-5">
          <h2 class="display-6 fw-bold text-uppercase mb-3">{{ lastRegisteredRoute }}</h2>
          <p class="fs-5">Tu marca ha pasado a revisión por el comité de guías.</p>
          <p class="text-secondary small mt-3 italic text-uppercase">La montaña es de todos, la responsabilidad es tuya.</p>
        </div>
        <div class="modal-footer border-0 justify-content-center pb-4">
          <button type="button" class="btn btn-primary px-5 py-2 fw-bold text-uppercase rounded-0" data-bs-dismiss="modal">Entendido</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue'
import { Modal } from 'bootstrap'

const imgCabecera = new URL('../assets/snowmountain.jpg', import.meta.url).href

const wasValidated = ref(false)
const modalElement = ref(null)
const lastRegisteredRoute = ref('')
let modalInstance = null

const initialState = {
  routeName: '',
  location: '',
  markerType: '',
  difficulty: '',
  gpsLink: '',
  length: '',
  elevation: null,
  duration: null,
  season: '',
  equipment: '',
  description: '',
  terms: false
}

const formData = reactive({ ...initialState })

onMounted(() => {
  modalInstance = new Modal(modalElement.value)
})

const handleSubmit = (event) => {
  const form = event.target
  wasValidated.value = true
  
  if (!form.checkValidity()) {
    return
  }

  lastRegisteredRoute.value = formData.routeName
  modalInstance.show()
  resetForm()
}

const resetForm = () => {
  Object.assign(formData, initialState)
  wasValidated.value = false
}
</script>

<style scoped>
.recorte-bandera {
  clip-path: polygon(0 0, 100% 0, 95% 50%, 100% 100%, 0 100%);
}

.cabecera {
  height: 300px;
  object-fit: cover;
}

.rounded-0 {
  border-radius: 0 !important;
}

.form-control, .form-select, .btn, .modal-content, .form-check-input {
  border-radius: 0 !important;

}

::placeholder {
  color: #a9adb1 !important;
  opacity: 1 !important;
}
.form-label {
  font-weight: 600;
  text-transform: uppercase;
  font-size: 0.75rem;
  letter-spacing: 1px;
  color: #adb5bd;
}

.form-control, .form-select {
  background-color: #2b3035;
  border: 1px solid #495057;
  color: white;
  transition: all 0.3s ease;
}

.form-control:focus {
  background-color: #343a40;
  color: white;
  border-color: #f8c52d;
  box-shadow: none;
}

.modal-content {
  border-left: 2px solid #f8c52d !important;
}
</style>