<script setup>
import { computed } from 'vue';

const props = defineProps({
  alerta: {
    type: Object,
    required: true,
  },
});

const isError = computed(() => {
  return props.alerta.tipo == 'error';
});
</script>

<template>
  <div
    :class="[isError ? 'alerta--error' : 'alerta--exito']"
    class="alerta"
  >
    {{ alerta.mensaje }}
  </div>
</template>

<style>
.alerta {
  margin: 1rem 0;
  font-size: 2rem;
  text-align: center;
  font-weight: 700;
  padding: 1rem 0;
  text-transform: capitalize;
  color: var(--negro);
}

.alerta--error {
  border-left: 0.5rem solid rgb(255, 1, 1);
  background-color: rgba(255, 1, 1, 0.2);
}

.alerta--exito {
  border-left: 0.5rem solid green;
  background-color: rgba(8, 234, 8, 0.2);
}
</style>
