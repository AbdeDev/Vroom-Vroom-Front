<template>
  <div class="p-6 bg-white shadow-lg rounded-lg">
    <!-- Onglets pour la durée et la distance -->
    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-6">
      <div class="p-6 bg-blue-500 text-white rounded-lg shadow-lg text-center">
        <h2 class="text-xl font-bold">Durée Totale</h2>
        <p class="text-lg font-semibold">{{ raceData.duration }} minutes</p>
      </div>
      <div class="p-6 bg-green-500 text-white rounded-lg shadow-lg text-center">
        <h2 class="text-xl font-bold">Distance Totale</h2>
        <p class="text-lg font-semibold">{{ raceData.distance }} km</p>
      </div>
    </div>

    <!-- Section du graphique -->
    <div class="bg-gray-100 p-6 shadow-lg rounded-lg mb-6">
      <canvas id="speedChart"></canvas>
    </div>

    <!-- Informations sur la vitesse -->
    <div class="flex flex-col sm:flex-row justify-between items-center">
      <div class="text-center sm:text-left mb-4 sm:mb-0">
        <p class="text-lg text-gray-700">Vitesse Max : <span class="font-semibold">{{ raceData.maxSpeed }} km/h</span></p>
        <p class="text-lg text-gray-700">Vitesse Min : <span class="font-semibold">{{ raceData.minSpeed }} km/h</span></p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted } from 'vue';
import { Chart, registerables } from 'chart.js';

Chart.register(...registerables);

export default defineComponent({
  name: 'RaceDetail',
  props: {
    raceData: {
      type: Object,
      required: true,
    },
  },
  setup(props) {
    onMounted(() => {
      const ctx = document.getElementById('speedChart') as HTMLCanvasElement;
      new Chart(ctx, {
        type: 'line',
        data: {
          labels: props.raceData.time,
          datasets: [
            {
              label: 'Vitesse (km/h)',
              data: props.raceData.speed,
              borderColor: 'rgb(75, 192, 192)',
              tension: 0.4,
              backgroundColor: 'rgba(75, 192, 192, 0.2)',
              fill: true,
            },
          ],
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          scales: {
            x: {
              title: {
                display: true,
                text: 'Temps (s)',
                color: 'rgb(75, 192, 192)',
              },
            },
            y: {
              title: {
                display: true,
                text: 'Vitesse (km/h)',
                color: 'rgb(75, 192, 192)',
              },
            },
          },
        },
      });
    });
  },
});
</script>

<style scoped>
#speedChart {
  width: 100%;
  height: 300px;
}
</style>
