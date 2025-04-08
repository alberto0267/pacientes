<script setup>
import { computed } from "vue";
const props = defineProps({
  alerta: {
    type: Object,
    required: true,
  },
});

const isError = computed(() => {
  return props.alerta.tipo === "error";
});
</script>

<template>
  <div
    :class="[isError ? 'bg-red-500' : 'bg-green-500']"
    class="text-white text-center p3 font-bold mb-3"
  >
    {{ alerta.mensaje }}
  </div>
</template>
