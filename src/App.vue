<script setup>
import { ref, reactive, watch, onMounted } from "vue";
import Header from "./components/Header.vue";
import Formulario from "./components/Formulario.vue";
import Paciente from "./components/Paciente.vue";
import { uid } from "uid";
const pacientes = ref([]);

const datos = reactive({
  id: null,
  nombre: "",
  propietario: "",
  email: "",
  alta: "",
  sintomas: "",
});

watch(
  pacientes,
  () => {
    guardarLocalStore();
  },
  {
    deep: true,
  }
);

const guardarLocalStore = () => {
  localStorage.setItem("pacientes", JSON.stringify(pacientes.value));
};

onMounted(() => {
  const pacientesStorage = localStorage.getItem("pacientes");
  if (pacientesStorage) {
    pacientes.value = JSON.parse(pacientesStorage);
  }
});

const guardarDatos = (id) => {
  if (datos.id) {
    const { id } = datos;
    const i = pacientes.value.findIndex(
      (pacienteState) => pacienteState.id === id
    );
    pacientes.value[i] = { ...datos };
  } else {
    pacientes.value.push({
      ...datos,
      id: uid(),
    });
  }

  // datos.nombre = "";
  // datos.propietario = "";
  // datos.email = "";
  // datos.alta = "";
  // datos.sintomas = "";

  Object.assign(datos, {
    id: null, // Reiniciamos el id para que el próximo paciente sea nuevo y no una edición
    nombre: "", // Limpiamos el campo nombre del formulario
    propietario: "", // Limpiamos el campo propietario
    email: "", // Limpiamos el campo email
    alta: "", // Limpiamos la fecha de alta
    sintomas: "", // Limpiamos los síntomas
    // En resumen: reiniciamos todo el formulario para dejarlo listo para un nuevo registro
  });
};

const editarDatos = (id) => {
  const pacienteEditado = pacientes.value.filter(
    (paciente) => paciente.id === id
  )[0];

  Object.assign(datos, pacienteEditado);
  console.log("editarDatoPaciente", id);
};

const eliminarPaciente = (id) => {
  pacientes.value = pacientes.value.filter((paciente) => paciente.id !== id);

  console.log("llegando el = " + id);
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
        :id="datos.id"
      />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">
          Administra tus pacientes
        </h3>
        <div v-if="pacientes.length > 0">
          <paciente
            v-for="paciente in pacientes"
            :paciente="paciente"
            @editar-datos="editarDatos"
            @eliminar-paciente="eliminarPaciente"
          />
        </div>
        <p v-else class="mt-10 text-2xl text-center">Esto es un desierto 😒</p>
      </div>
    </div>
  </div>
</template>
