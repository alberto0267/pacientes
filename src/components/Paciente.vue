<script setup>
defineProps({
  paciente: {
    type: Object,
    required: true,
  },
});
// defineEmits[("editar-datos", "eliminar-paciente")];
defineEmits("editar-datos", "eliminar-paciente");
</script>

<template>
  <div class="mx-5 my-10 bg-white shadow-md px-5 py-10 rounded-xl">
    <p class="font-bold mb-3 text-gray-700 uppercase">
      ID:
      {{ paciente.id }}
      <span class="font-normal normal-case"> </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">
      Nombre:
      {{ paciente.nombre }}
      <span class="font-normal normal-case"> </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">
      Propietario:
      {{ paciente.propietario }}
      <span class="font-normal normal-case"> </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">
      Email:
      {{ paciente.email }}
      <span class="font-normal normal-case"> </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">
      Alta:
      {{ paciente.alta }}
      <span class="font-normal normal-case"> </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">
      Sintomas:
      {{ paciente.sintomas }}
      <span class="font-normal normal-case"> </span>
    </p>

    <div class="grid md:grid-cols-2 gap-5 mt-10">
      <button
        type="button"
        class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg"
        @click="$emit('editar-datos', paciente.id)"
      >
        Editar
      </button>

      <button
        type="button"
        class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg"
        @click="$emit('eliminar-paciente', paciente.id)"
      >
        Eliminar
      </button>
    </div>
  </div>
</template>

<style scoped></style>
