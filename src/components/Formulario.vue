<script setup>
import { reactive, computed } from 'vue';

import Alerta from './Alerta.vue';

const emit = defineEmits([
  'update:nombre',
  'update:capitulos',
  'update:year',
  'update:resumen',
  'guardar-anime',
]);

const props = defineProps({
  id: {
    type: [String, null],
  },
  nombre: {
    type: String,
    required: true,
  },
  capitulos: {
    type: Number,
    required: true,
  },
  year: {
    type: Number,
    required: true,
  },
  resumen: {
    type: String,
    required: true,
  },
});

const alerta = reactive({
  tipo: '',
  mensaje: '',
});

const validar = () => {
  if (
    Object.values(props).includes('') ||
    props.capitulos <= 0 ||
    props.year <= 0
  ) {
    alerta.mensaje = 'Todos los campos son Obligatorios';
    alerta.tipo = 'error';
    return;
  }

  emit('guardar-anime');
  alerta.mensaje = 'El anime se guardo correctamente';
  alerta.tipo = 'exito';

  setTimeout(() => {
    Object.assign(alerta, {
      tipo: '',
      mensaje: '',
    });
  }, 2500);
};

const editando = computed(() => {
  return props.id;
});
</script>

<template>
  <div class="formulario">
    <h2 class="formulario__titulo">
      Agrega los <span>animes</span> que has visto este año
    </h2>

    <Alerta
      v-if="alerta.mensaje"
      :alerta="alerta"
    />

    <form
      class="formulario__form"
      @submit.prevent="validar"
    >
      <div class="formulario__campo">
        <label
          class="formulario__label"
          for="nombre"
          >Nombre del anime</label
        >
        <input
          class="formulario__input"
          type="text"
          id="nombre"
          placeholder="Nombre del anime"
          :value="nombre"
          @input="$emit('update:nombre', $event.target.value)"
        />
      </div>

      <div class="formulario__campo">
        <label
          class="formulario__label"
          for="capitulos"
          >Número de capitulos</label
        >
        <input
          class="formulario__input"
          type="number"
          id="capitulos"
          min="0"
          :value="capitulos"
          @input="$emit('update:capitulos', +$event.target.value)"
        />
      </div>

      <div class="formulario__campo">
        <label
          class="formulario__label"
          for="year"
          >Año de visualizacion</label
        >
        <input
          class="formulario__input"
          type="number"
          name="year"
          min="2022"
          :value="year"
          @input="$emit('update:year', +$event.target.value)"
        />
      </div>

      <div class="formulario__campo">
        <label
          class="formulario__label"
          for="resumen"
          >Resúmen</label
        >
        <textarea
          cols="30"
          rows="8"
          wrap="hard"
          class="formulario__textarea"
          name="resumen"
          id="resumen"
          :value="resumen"
          @input="$emit('update:resumen', $event.target.value)"
        ></textarea>
      </div>

      <input
        class="formulario__submit"
        type="submit"
        :value="[editando ? 'Guardar Cambios' : 'Guardar Anime']"
      />
    </form>
  </div>
</template>

<style>
.formulario {
  margin-bottom: 5rem;
}

@media (min-width: 768px) {
  .formulario {
    flex: 1;
  }
}

.formulario__titulo {
  text-align: center;
  padding: 1rem 0;
}

.formulario__form {
  margin: 1rem 0;
}
.formulario__campo {
  display: flex;
  flex-direction: column;
}

.formulario__label {
  font-size: 2.2rem;
  padding: 1rem 0;
}

.formulario__input {
  all: unset;
  padding: 1rem;
  border: 1px solid #0e0e0e;
  border-radius: 0.5rem;
}

.formulario__textarea {
  padding: 1rem 2rem;
  border: 1px solid #0e0e0e;
  border-radius: 0.5rem;
  height: 10rem;
}

.formulario_descripcion {
  margin: 1rem 0 0 0;
}

.formulario__submit {
  all: unset;
  width: 100%;
  margin: 1rem 0;
  padding: 1rem 0;
  text-align: center;
  background-color: rgb(50, 209, 209);
  color: var(--blanco);
  font-size: 2rem;
  font-weight: 700;
  border-radius: 1rem;
}

.formulario__submit:hover {
  background-color: rgb(18, 110, 110);
  cursor: pointer;
}
</style>
