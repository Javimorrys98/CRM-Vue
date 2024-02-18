<script setup>
import axios from 'axios'
import RouterLink from '../components/UI/RouterLink.vue';
import Heading from '../components/UI/Heading.vue'
import { FormKit } from '@formkit/vue'

const props = defineProps({
    titulo: {
        type: String,
        required: true
    }
})

const handleSubmit = (data) => {
    axios.post("http://localhost:4000/clientes", data)
        .then(respuesta => console.log(respuesta))
        .catch(error => console.log("Hubo un error."))
}
</script>

<template>
    <div>
        <div>
            <div class="flex justify-end">
                <RouterLink to="inicio">
                    Volver
                </RouterLink>
            </div>
        </div>
        <Heading>{{ titulo }}</Heading>
        <div class="mx-auto mt-10 bg-white shadow">
            <div class="mx-auto md:w-4/5 py-20 px-6">
                <FormKit type="form" submit-label="Agregar cliente"
                    incomplete-message="No se pudo enviar, revisa los mensajes." @submit="handleSubmit">
                    <FormKit type="text" name="nombre" label="Nombre" placeholder="Nombre del cliente..."
                        validation="required"
                        :validation-messages="{ required: 'El nombre del cliente es obligatorio.' }" />
                    <FormKit type="text" name="apellido" label="Apellido" placeholder="Apellido del cliente..."
                        validation="required"
                        :validation-messages="{ required: 'El apellido del cliente es obligatorio.' }" />
                    <FormKit type="text" name="email" label="Email" placeholder="Email del cliente..."
                        validation="required|email"
                        :validation-messages="{ required: 'El email del cliente es obligatorio.', email: 'Coloca un email válido' }" />
                    <FormKit type="text" name="telefono" label="Teléfono" placeholder="Teléfono: XXX-XXX-XXXX"
                        validation="*matches:/^[0-9]{3}-[0-9]{3}-[0-9]{4}$/"
                        :validation-messages="{ matches: 'El formato del teléfono no es válido.' }" />
                    <FormKit type="text" name="empresa" label="Empresa" placeholder="Empresa del cliente..." />
                    <FormKit type="text" name="puesto" label="Puesto" placeholder="Puesto del cliente..." />
                </FormKit>
            </div>
        </div>
    </div>
</template>

<style>
.formkit-wrapper {
    max-width: 100%;
}
</style>