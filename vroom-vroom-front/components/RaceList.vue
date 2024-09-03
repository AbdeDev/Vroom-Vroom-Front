<template>
    <aside class="w-full md:w-1/4 bg-white p-6 h-full md:h-screen overflow-y-auto shadow-lg">
      <h2 class="text-2xl font-bold text-gray-700 mb-6">Courses Passées</h2>
      <ul>
        <li
          v-for="race in races"
          :key="race.id"
          @click="selectRace(race)"
          class="cursor-pointer p-4 mb-4 bg-gray-100 hover:bg-gray-200 rounded-lg transition-all duration-200 shadow-sm hover:shadow-md"
        >
          <div class="flex justify-between items-center">
            <span class="text-lg font-semibold text-gray-700">{{ race.name }}</span>
            <span class="text-sm text-gray-500">{{ race.date }}</span>
          </div>
        </li>
      </ul>
    </aside>
  </template>
  
  <script lang="ts">
  import { defineComponent } from 'vue';
  
  export default defineComponent({
    name: 'RaceList',
    data() {
      return {
        races: [
          {
            id: 1,
            name: 'Course 1',
            date: '2024-01-01',
            data: {
              speed: [20, 40, 60, 80, 100, 120],
              time: ['0s', '10s', '20s', '30s', '40s', '50s'],
              distance: 50,
              duration: 60,
              maxSpeed: 120,
              minSpeed: 20,
            },
          },
          // Ajoutez d'autres courses ici
        ]
      };
    },
    methods: {
      selectRace(race :any) {
        this.$emit('select-race', race);
      },
    },
  });
  </script>
  
  <style scoped>
  /* Styles supplémentaires si nécessaire */
  </style>
  