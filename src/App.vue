<script setup>
import { reactive, ref, onMounted, watch } from 'vue';
import { generarId } from './utils';

import Header from './components/Header.vue';
import Formulario from './components/Formulario.vue';
import Anime from './components/Anime.vue';

const anime = reactive({
  id: null,
  nombre: '',
  capitulos: 0,
  year: 2022,
  resumen: '',
});

const animes = ref([]);

watch(
  animes,
  () => {
    guardarLocalStorage();
  },
  {
    deep: true,
  }
);

//* Local Storage
const guardarLocalStorage = () => {
  localStorage.setItem('animes', JSON.stringify(animes.value));
};

onMounted(() => {
  const animesStorage = localStorage.getItem('animes');

  if (animesStorage) {
    animes.value = JSON.parse(animesStorage);
  }
});

const guardarAnime = () => {
  if (anime.id) {
    const { id } = anime;
    const i = animes.value.findIndex((anime) => anime.id === id);
    animes.value[i] = { ...anime };
  } else {
    animes.value.push({ ...anime, id: generarId() });
  }
  Object.assign(anime, {
    id: null,
    nombre: '',
    capitulos: 0,
    year: 2022,
    resumen: '',
  });
};

const actualizarAnime = (id) => {
  const animeEditar = animes.value.filter((anime) => anime.id === id)[0];
  Object.assign(anime, animeEditar);
};

const eliminarAnime = (id) => {
  animes.value = animes.value.filter((anime) => anime.id !== id);
};
</script>

<template>
  <Header />

  <div class="contenedor principal">
    <Formulario
      v-model:nombre="anime.nombre"
      v-model:capitulos="anime.capitulos"
      v-model:year="anime.year"
      v-model:resumen="anime.resumen"
      @guardar-anime="guardarAnime"
      :id="anime.id"
    />

    <div class="admin">
      <h2 class="admin__titulo">Animes Vistos en <span>2023</span></h2>

      <div class="lista">
        <Anime
          v-for="anime in animes"
          :anime="anime"
          @actualizar-anime="actualizarAnime"
          @eliminar-anime="eliminarAnime"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.principal {
  display: flex;
  flex-direction: column;
}

@media (min-width: 768px) {
  .principal {
    flex-direction: row;
  }
  .admin {
    flex: 2;
  }
}

.admin__titulo {
  text-align: center;
}

.lista {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
}

@media (min-width: 768px) {
  .lista {
    padding: 5rem;
    gap: 5rem;
  }
}
</style>
