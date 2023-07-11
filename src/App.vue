<script setup>
  import {RouterView} from 'vue-router'
</script>

<template>
  <header class="bg-teal-500">
    <div class="mx-auto max-w-6xl py-10">
      <h1 class="font-extrabold text-white text-4xl">Administrador Clientes</h1>
    </div>
  </header>

  <div class="mx-auto max-w-6xl mt-10">
    <RouterView />
  </div>

</template>
