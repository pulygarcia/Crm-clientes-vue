<script setup>
    import { onMounted, ref } from 'vue';
    import {useRouter, useRoute} from 'vue-router';
    import ClienteServices from '../services/ClienteServices';
    import RouterLink  from '../components/UI/RouterLink.vue';
    import Heading  from '../components/UI/Heading.vue';

    const router = useRouter();
    const route = useRoute();

    const {id} = route.params; //Extraer el id por url

    const clienteData = ref({})

    onMounted(() => {
        ClienteServices.obtenerCliente(id)
            .then(({data}) => {
                clienteData.value = data;
            })
            .catch(error => console.log(error))
    })

    defineProps({
        titulo: String
    })

    const handleSubmit = (data) => {
        ClienteServices.actualizarCliente(id, data)
            .then(resultado => router.push({name: 'inicio'}))
            .catch(error => console.log(error))
    }
</script>

<template>
  <div>
    <div class="flex justify-end">
        <RouterLink to="inicio">Listado clientes</RouterLink>
    </div>

    <Heading>{{ titulo }}</Heading>

    <div class="mt-10 mx-auto bg-white shadow-lg">
        <div class="mx-auto p-6 md:w-2/3">
            <FormKit 
                type="form"
                :actions="false" 
                incomplete-message="Por favor revisa los campos"
                @submit="handleSubmit"
            >
                <FormKit
                type="text"
                name="nombre"
                id="nombre"
                validation="required"
                :validation-messages="{required: 'El nombre es obligatorio'}"
                label="Nombre del cliente"
                placeholder="“José Ignacio”"
                v-model="clienteData.nombre"
                />

                <FormKit
                type="text"
                label="Apellido"
                name="apellido"
                id="apellido"
                placeholder="Ingresar apellido"
                v-model="clienteData.apellido"
                />

                <FormKit
                type="email"
                label="Correo Electrónico"
                validation="required|*email"
                validation-visibility="live"
                :validation-messages="{required: 'Email es obligatorio', email: 'Ingresa un email válido'}"
                name="email"
                id="email"
                placeholder="correo@gmail.com"
                v-model="clienteData.email"
                />

                <FormKit
                type="text"
                label="Teléfono"
                validation="matches:/^[0-9]{3}-[0-9]{3}-[0-9]{4}$/"
                validation-visibility="live"
                :validation-messages="{matches: 'Teléfono no válido'}"
                name="telefono"
                id="telefono"
                placeholder="Teléfono: XXX-XXX-XXXX"
                v-model="clienteData.telefono"
                />

                <FormKit
                type="text"
                label="Empresa"
                name="empresa"
                id="empresa"
                placeholder="Antonio banderas inc."
                v-model="clienteData.empresa"
                />

                <FormKit
                type="text"
                label="Puesto"
                name="puesto"
                id="puesto"
                placeholder="Empleado"
                v-model="clienteData.puesto"
                />

                <FormKit
                type="submit"
                label="Agregar cliente"
                />

            </FormKit>
        </div>
    </div>
  </div>
</template>

<style>
    .formkit-wrapper{
        max-width: 100%;
    }
</style>