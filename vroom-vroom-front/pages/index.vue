<template>
  <div class="min-h-screen bg-gray-100">
    <!-- Include the Header Component -->
    <Header />
    
    <!-- Contenu principal -->
    <div class="flex flex-col md:flex-row">
      <!-- RaceList Component -->
      <RaceList @select-race="handleRaceSelection" />
      
      <!-- RaceDetail Component -->
      <div v-if="selectedRace" class="w-full md:w-3/4 bg-white p-4">
        <RaceDetail :raceData="selectedRace.data" />
      </div>
      <div v-else class="w-full md:w-3/4 bg-white p-4 flex items-center justify-center">
        <p class="text-gray-500">Sélectionnez une course pour voir les détails.</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Header from '~/components/Header.vue';
import RaceList from '~/components/RaceList.vue';
import RaceDetail from '~/components/RaceDetail.vue';

export default defineComponent({
  name: 'Index',
  components: {
    Header,
    RaceList,
    RaceDetail,
  },
  data() {
    return {
      selectedRace: null,
    };
  },
  methods: {
    handleRaceSelection(race : any) {
      this.selectedRace = race;
    },
  },
});
</script>

<style scoped>
/* Styles supplémentaires si nécessaire */
</style>
