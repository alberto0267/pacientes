<script setup>
import { ref, reactive } from "vue";
import Alerta from "./Alerta.vue";
// Con ref se podria hacer pero es solo par aun elemento, aqui es cuanod aplica reactive
// const nombre1 = ref("");
// const nombre = reactive("");

// const nombreInput = document.querySelector("#input");

// nombreInput.addEventListener("input", (e) => {
//   console.log(e.target.value);
// });

// const leerNombre = (e) => {
//   nombre.value = e.targe.value;
// };

const alerta = reactive({
  tipo: "",
  mensaje: "",
});

// aqui lo definimos en variable para poder usarlo en validar
const emit = defineEmits([
  "update:nombre",
  "update:propietario",
  "update:email",
  "update:alta",
  "update:sintomas",
  "guardar-datos",
]);

const props = defineProps({
  nombre: {
    type: String,
    required: true,
  },
  propietario: {
    type: String,
    required: true,
  },
  email: {
    type: String,
    required: true,
  },
  alta: {
    type: String,
    required: true,
  },
  sintomas: {
    type: String,
    required: true,
  },
});
// Objects.values coge los datos del objeto
const validar = () => {
  if (Object.values(props).includes("")) {
    alerta.tipo = "error";
    alerta.mensaje = "TODOS LOS CAMPOS SON OBLIGATORIOS";

    console.log("Esta vacio");
    return;
  }
  emit("guardar-datos");
  alerta.mensaje = "PACIENTE GUARDADO CORRECTAMENTE";
  alerta.tipo = "sucess";
  console.log("aplica el sucess");
  setTimeout(() => {
    Object.assign(alerta, {
      tipo: "",
      mensaje: "",
    });
  }, 3000);
};
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-bold text-center">Seguimiento Pacientes</h2>
    <p class="text-lg mt-5 mb-10 text-center">
      Añade pacientes y
      <span class="text-indigo-600 font-bold">Administralos</span>
    </p>

    <Alerta v-if="alerta.mensaje" :alerta="alerta" />

    <form
      class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
      @submit.prevent="validar"
    >
      <div class="mb-5">
        <label for="mascota" class="block text-gray-700 uppercase font-bold"
          >Nombre Mascota</label
        >
        <input
          type="text"
          id="mascota"
          placeholder="Nombre mascota"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          :value="nombre"
          @input="$emit('update:nombre', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="propietario" class="block text-gray-700 uppercase font-bold"
          >NOMBRE PROPIETARIO</label
        >
        <input
          type="text"
          id="propietario"
          placeholder="Nombre Propietario"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          @input="$emit('update:propietario', $event.target.value)"
          :value="propietario"
        />
      </div>

      <div class="mb-5">
        <label for="email" class="block text-gray-700 uppercase font-bold"
          >EMAIL</label
        >
        <input
          type="email"
          id="email"
          placeholder="Email del Propietario"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          @input="$emit('update:email', $event.target.value)"
          :value="email"
        />
      </div>

      <div class="mb-5">
        <label for="alta" class="block text-gray-700 uppercase font-bold"
          >ALTA</label
        >
        <input
          type="date"
          id="alta"
          placeholder=""
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
          @input="$emit('update:alta', $event.target.value)"
          :value="alta"
        />
      </div>

      <div class="mb-5">
        <label for="sintomas" class="block text-gray-700 uppercase font-bold"
          >SINTOMAS</label
        >
        <textarea
          id="sintomas"
          placeholder=""
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-40"
          @input="$emit('update:sintomas', $event.target.value)"
          :value="sintomas"
        />
      </div>
      <input
        type="submit"
        class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
        value="REGISTRAR PACIENTE"
      />
    </form>
  </div>
</template>
