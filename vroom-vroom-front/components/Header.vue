<template>
    <header class="bg-gradient-to-r from-blue-600 to-indigo-600 text-white p-6 shadow-lg">
      <div class="container mx-auto flex flex-col md:flex-row justify-between items-center">
        <h1 class="text-3xl font-extrabold">VroomVroom</h1>
        <h2 class="text-xl font-semibold mt-2 md:mt-0">Résumé de course</h2>
      </div>
    </header>
  </template>
  
  <script lang="ts">
  import { defineComponent } from 'vue';
  
  export default defineComponent({
    name: 'Header',
  });
  </script>
  
  <style scoped>
  /* Styles supplémentaires pour le header */
  </style>
  