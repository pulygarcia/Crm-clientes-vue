<script setup>
    import { computed } from 'vue';
    import {RouterLink} from 'vue-router';

    const props = defineProps({
        cliente: {
            type: Object,
            required: true
        }
    })

    defineEmits(['actualizar-estado', 'eliminar-cliente'])

    const nombreApellido = computed(() => {
      return props.cliente.nombre + ' ' + props.cliente.apellido;
    })

    const estadoCliente = computed(() => {
      return props.cliente.estado > 0;
    })
</script>

<template>
  <tr>
        <td class="whitespace-nowrap py-4 pl-4 pr-3 text-sm sm:pl-0">
            <p class="font-medium text-gray-900">{{ nombreApellido }}</p>  <!--usando el computed para concatenar nombre y apellido sin tener que abrir llaves dos veces {} {}-->
            <p class="text-gray-500">{{ cliente.email }}</p>
        </td>
        <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
            <p class="text-gray-900 font-bold">{{ cliente.empresa }}</p>
            <p class="text-gray-600">{{ cliente.puesto }}</p>
        </td>
        <td class="whitespace-nowrap px-3 py-4 text-sm">
          <button 
            class="rounded-full font-semibold text-xs p-2"
            :class="estadoCliente ? 'bg-green-200 text-green-600' : 'bg-red-200 text-red-500'"
            @click="$emit('actualizar-estado', {id: cliente.id, estado: cliente.estado})"
          >
            {{ estadoCliente ? 'Activo' : 'Inactivo' }}
          </button>
        </td>
        <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500 ">
          <RouterLink 
            :to="{name: 'editar-cliente', params: {id: cliente.id}}"
            class="text-indigo-500 hover:text-indigo-800"
          >
            Editar
          </RouterLink>

          <RouterLink 
            to="/"
            class="text-red-600 ms-2"
            @click="$emit('eliminar-cliente', cliente.id)"
          >
            Eliminar
          </RouterLink>
        </td>
    </tr>
</template>