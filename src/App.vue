<script setup>
import { ref, reactive } from "vue";

import Header from "./components/Header.vue";
import Formulario from "./components/Formulario.vue";
const pacientes = ref([]);
const datos = reactive({
  nombre: "",
  propietario: "",
  email: "",
  alta: "",
  sintomas: "",
});

const guardarDatos = () => {
  console.log("agregando...");
  pacientes.value.push(datos);
};
</script>
<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex">
      <Formulario
        v-model:nombre="datos.nombre"
        v-model:propietario="datos.propietario"
        v-model:email="datos.email"
        v-model:alta="datos.alta"
        v-model:sintomas="datos.sintomas"
        @guardar-datos="guardarDatos"
      />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">
          Administra tus pacientes
        </h3>
        <div v-if="pacientes.legth > 0"></div>
        <p v-else class="mt-10 text-2xl text-center">Esto es un desierto 😒</p>
      </div>
    </div>
  </div>
</template>
