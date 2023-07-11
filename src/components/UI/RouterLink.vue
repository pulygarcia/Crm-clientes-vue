<script setup>
    import { RouterLink } from 'vue-router';

    defineProps({
        to:{
            type: String,
            required: true
        }
    })
</script>

<template>

    <RouterLink 
        :to="{name: to}"
        class="bg-sky-600 text-white text-xl mb-6 inline-block font-bold p-2 rounded-lg shadow-sm hover:bg-sky-700 transition"
    >
        <slot></slot>
    </RouterLink>

</template>