<script setup>
    import { computed } from 'vue';
    import {RouterLink} from 'vue-router';

    const props = defineProps({
        cliente: {
            type: Object,
            required: true
        }
    })

    const nombreApellido = computed(() => {
      return props.cliente.nombre + ' ' + props.cliente.apellido;
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
          <p :class="cliente.estado === 1 ? 'text-green-500' : 'text-gray-600'">{{ cliente.estado === 1 ? 'Activo' : 'Inactivo'}}</p>
        </td>
        <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500 ">
          <RouterLink 
            to="/"
            class="text-indigo-500 hover:text-indigo-800"
          >
            Editar
          </RouterLink>

          <RouterLink 
            to="/"
            class="text-red-600 ms-2"
          >
            Eliminar
          </RouterLink>
        </td>
    </tr>
</template>