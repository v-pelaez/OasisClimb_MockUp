<template>
  <section id="ranking" class="py-5">
    <div class="row col-12 bg-primary text-black text-uppercase p-5 recorte-bandera">
      <h3 class="fw-bold fst-italic">Rankings</h3>
    </div>

    <div class="container my-4">
      <ul class="nav nav-tabs" id="rankingTabs" role="tablist">
        <li v-for="tab in rankings" :key="tab.id" class="nav-item" role="presentation">
          <button
            class="nav-link"
            :class="{ active: activeTab === tab.id }"
            @click="activeTab = tab.id"
            type="button"
            role="tab"
            :aria-selected="activeTab === tab.id"
          >
            {{ tab.title }}
          </button>
        </li>
      </ul>

      <div class="tab-content mt-3" id="rankingTabsContent">
        <div
          v-for="tab in rankings"
          :key="tab.id"
          class="tab-pane fade"
          :class="{ 'show active': activeTab === tab.id }"
          role="tabpanel"
        >
          <div class="table-responsive">
            <table class="table table-striped table-bordered align-middle">
              <thead class="table-dark">
                <tr>
                  <th v-for="header in tab.headers" :key="header">{{ header }}</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="row in tab.data" :key="row.rank">
                  <td class="fw-bold">{{ row.rank }}</td>
                  <td>{{ row.name }}</td>
                  <td>{{ row.country }}</td>
                  <td >
                    <span class="badge bg-primary text-black">{{ row.metric }}</span>
                  </td>
                  <td>{{ row.points }}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

// Estado para controlar la pestaña activa (por defecto la primera)
const activeTab = ref('dificultad')

const rankings = ref([
  {
    id: 'dificultad',
    title: 'Ranking de dificultad',
    headers: ['#', 'Escalador', 'País', 'Dificultad Máxima', 'Puntos'],
    data: [
      { rank: 1, name: 'Alberto Ginés', country: '🇪🇸 España', metric: '9a+', points: 4485 },
      { rank: 2, name: 'Jan Novak', country: '🇨🇿 República Checa', metric: '9a', points: 4200 },
      { rank: 3, name: 'Li Wei', country: '🇨🇳 China', metric: '8c+', points: 4150 },
      { rank: 4, name: 'Thomas Berger', country: '🇦🇹 Austria', metric: '8c', points: 4100 },
      { rank: 5, name: 'Satone Yoshida', country: '🇯🇵 Japón', metric: '9a', points: 4130 },
      { rank: 6, name: 'Elena Rossi', country: '🇮🇹 Italia', metric: '8c+', points: 3900 },
      { rank: 7, name: 'Ivan Petrov', country: '🇧🇬 Bulgaria', metric: '8c', points: 3800 },
      { rank: 8, name: 'Simona Kolarova', country: '🇸🇰 Eslovaquia', metric: '8b+', points: 3700 },
      { rank: 9, name: 'Markus Huber', country: '🇨🇭 Suiza', metric: '8b+', points: 3600 },
      { rank: 10, name: 'Lucas García', country: '🇦🇷 Argentina', metric: '8b', points: 3500 },
    ],
  },
  {
    id: 'velocidad',
    title: 'Ranking de velocidad',
    headers: ['#', 'Escalador', 'País', 'Mejor Tiempo', 'Puntos'],
    data: [
      { rank: 1, name: 'Martina López', country: '🇪🇸 España', metric: '5.15 s', points: 1000 },
      { rank: 2, name: 'David Novak', country: '🇨🇿 República Checa', metric: '5.34 s', points: 970 },
      { rank: 3, name: 'Chen Yu', country: '🇨🇳 China', metric: '5.42 s', points: 950 },
      { rank: 4, name: 'Stefan Müller', country: '🇦🇹 Austria', metric: '5.55 s', points: 920 },
      { rank: 5, name: 'Chiara Bianchi', country: '🇮🇹 Italia', metric: '5.60 s', points: 910 },
      { rank: 6, name: 'Jordi Sánchez', country: '🇪🇸 España', metric: '5.68 s', points: 895 },
      { rank: 7, name: 'Katerina Novakova', country: '🇨🇿 República Checa', metric: '5.72 s', points: 880 },
      { rank: 8, name: 'Yuan Fang', country: '🇨🇳 China', metric: '5.80 s', points: 860 },
      { rank: 9, name: 'Markus Steiner', country: '🇨🇭 Suiza', metric: '5.85 s', points: 845 },
      { rank: 10, name: 'Anna Müller', country: '🇩🇪 Alemania', metric: '5.90 s', points: 830 },
    ],
  },
])
</script>

<style scoped>
.recorte-bandera {
  clip-path: polygon(0 0, 100% 0, 95% 50%, 100% 100%, 0 100%);
  margin-bottom: 2rem;
}

.table {
  background-color: white;
}

.nav-link {
  cursor: pointer;
  transition: all 0.3s ease;
}

/* Mejora visual para la pestaña activa */
.nav-link.active {
  font-weight: bold;
  border-bottom: 3px solid #f8c52d !important;
}
</style>