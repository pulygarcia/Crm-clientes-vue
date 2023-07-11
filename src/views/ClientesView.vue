<script setup>
    import RouterLink from '../components/UI/RouterLink.vue';
    import Heading from '../components/UI/Heading.vue';

    defineProps({
        titulo: String
    })
</script>

<template>
  <div class="flex justify-end">
        <RouterLink to="agregar-cliente">
            Nuevo Cliente
        </RouterLink>
    </div>
    
    <Heading>{{ titulo }}</Heading>
</template>