<script setup>
defineEmits(['actualizar-anime', 'eliminar-anime']);

defineProps({
  anime: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div class="anime">
    <p class="anime__elemento">
      <span class="anime__span anime__span--titulo">{{ anime.nombre }}</span>
    </p>
    <p class="anime__elemento">
      ID: <span class="anime__span">{{ anime.id }}</span>
    </p>
    <p class="anime__elemento">
      Número de capitulos:
      <span class="anime__span">{{ anime.capitulos }}</span>
    </p>
    <p class="anime__elemento">
      Año de visualizacion: <span class="anime__span">{{ anime.year }}</span>
    </p>
    <p class="anime__elemento">
      Resúmen:
      <span class="anime__span">{{ anime.resumen }} </span>
    </p>

    <div class="anime__acciones">
      <button
        class="anime__boton anime__boton--naranja"
        @click="$emit('actualizar-anime', anime.id)"
      >
        <img
          src="/img/editar.svg"
          alt=""
        />Editar
      </button>
      <button
        class="anime__boton anime__boton--rojo"
        @click="$emit('eliminar-anime', anime.id)"
      >
        <img
          class="imagen__boton"
          src="/img/trash.svg"
          alt=""
        />Eliminar
      </button>
    </div>
  </div>
</template>

<style>
.anime {
  -webkit-box-shadow: 0px 1px 1px 1px rgba(11, 227, 255, 0.75);
  -moz-box-shadow: 0px 1px 1px 1px rgba(0, 195, 254, 0.75);
  box-shadow: 0px 1px 1px 1px rgba(32, 177, 255, 0.75);

  padding: 1rem 2rem;
}

.anime__elemento {
  font-size: 1.6rem;
  color: rgb(234, 98, 45);
}

.anime__span {
  display: block;
  font-size: 1.8rem;
  color: var(--negro);
}

.anime__span--titulo {
  text-align: center;
  font-weight: 700;
}

.anime__acciones {
  display: flex;
  justify-content: space-evenly;
}

.anime__boton {
  all: unset;
  display: flex;
  align-items: center;
  font-weight: 700;
  padding: 0.5rem 2rem;
}

.anime__boton--rojo {
  color: rgb(235, 21, 21);
  transition: all 0.3s ease;
}

.anime__boton--rojo:hover {
  border: 1px solid red;
  cursor: pointer;
}

.anime__boton--naranja {
  color: rgb(255, 145, 0);
  transition: all 0.3s ease;
}

.anime__boton--naranja:hover {
  border: 1px solid rgb(255, 145, 0);
  cursor: pointer;
}
</style>
