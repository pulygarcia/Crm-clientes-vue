<script setup>
    import {useRouter} from 'vue-router';
    import ClienteServices from '../services/ClienteServices';
    import RouterLink  from '../components/UI/RouterLink.vue';
    import Heading  from '../components/UI/Heading.vue';

    const router = useRouter();

    defineProps({
        titulo: String
    })

    const handleSubmit = (data) => {
        data.estado = 1;
        ClienteServices.agregarCliente(data)
            .then(resultado => {
                //redireccionar
                router.push({name: 'inicio'})
            })
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
                />

                <FormKit
                type="text"
                label="Apellido"
                name="apellido"
                id="apellido"
                placeholder="Ingresar apellido"
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
                />

                <FormKit
                type="text"
                label="Empresa"
                name="empresa"
                id="empresa"
                placeholder="Antonio banderas inc."
                />

                <FormKit
                type="text"
                label="Puesto"
                name="puesto"
                id="puesto"
                placeholder="Empleado"
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