<script setup>
    import { useRouter } from 'vue-router';
    import { onMounted, ref, computed } from 'vue';
    import ClienteServices from '../services/ClienteServices';
    import RouterLink from '../components/UI/RouterLink.vue';
    import Heading from '../components/UI/Heading.vue';
    import Cliente from '../components/Cliente.vue';

    const clientes = ref([]);

    const router = useRouter()

    defineProps({
        titulo: String
    })

    onMounted(() => {
        ClienteServices.obtenerClientes()
            .then(({data}) => {
                clientes.value = data;
            })
            .catch(error => console.log(error))
    })

    const hayClientes = computed(() => {
        return clientes.value.length > 0;
    })

    const actualizarEstado = (datosCliente) => {
        ClienteServices.actualizarEstado(datosCliente.id, {estado: !datosCliente.estado})
            .then(() => {
                const cliente = clientes.value.filter(cliente => cliente.id === datosCliente.id)[0];
                cliente.estado = !cliente.estado;
            })
            .catch(error => console.log(error))
    }

    const eliminarCliente = (id) =>{
        ClienteServices.eliminarCliente(id)
            .then(() => {
                clientes.value = clientes.value.filter(cliente => cliente.id !== id)
            })
            .catch(error => console.log(error))
    }
</script>

<template>
  <div class="flex justify-end">
        <RouterLink to="agregar-cliente">
            Nuevo Cliente
        </RouterLink>
    </div>
    
    <Heading>{{ titulo }}</Heading>

    <div v-if="hayClientes" class="flow-root mx-auto  mt-10 p-5 bg-white shadow">
      <div class="-my-2 -mx-4 overflow-x-auto sm:-mx-6 lg:-mx-8">
          <div class="min-w-full py-2 align-middle sm:px-6 lg:px-8">
              <table class="min-w-full divide-y divide-gray-300">
                  <thead>
                  <tr>
                      <th scope="col" class="p-2 text-left text-sm font-extrabold text-gray-600">Nombre</th>
                      <th scope="col" class="p-2 text-left text-sm font-extrabold text-gray-600">Empresa</th>
                      <th scope="col" class="p-2 text-left text-sm font-extrabold text-gray-600">Estado</th>
                      <th scope="col" class="p-2 text-left text-sm font-extrabold text-gray-600">Acciones</th>
                  </tr>
                  </thead>
                  <tbody class="divide-y divide-gray-200 bg-white">
                    <Cliente 
                        v-for="cliente in clientes"
                        :cliente="cliente"
                        :key="cliente.id"
                        @actualizar-estado="actualizarEstado"
                        @eliminar-cliente="eliminarCliente"
                    />
                  </tbody>
              </table>
          </div>
      </div>
  </div>
    <p v-else class="mt-20 text-center text-2xl">No hay clientes</p>
</template>