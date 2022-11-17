<template>
  <div class="h-screen bg-[#395144]">
    <div class="h-52 w-72 mx-auto">
      <img src="./assets/Logo_breaking_bad.png" />
    </div>
    <MiBuscador @enviaRespuesta="cargarpersonajes" />
    <div v-if="loading">
      <MiSpinner :elemento="this.filtrar_por" />
    </div>
    <div
      v-else
      class="bg-[#395144] overflow-y-scroll grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3"
    >
      <div class="col-span-1 lg:col-span-2">
        <MiLista :lista="listaPersonajes" @aFavs="anhadir" />
      </div>
      <div>
        <MiListaFav :lista="listaPersonajesFav" @eliminar="eliminarPersonaje" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import MiBuscador from "./components/MiBuscador.vue";
import MiLista from "./components/MiLista.vue";
import MiListaFav from "./components/MiListaFav.vue";
import MiSpinner from "./components/MiSpinner.vue";
export default {
  name: "App",
  data() {
    return {
      listaPersonajes: [],
      listaPersonajesFav: JSON.parse(localStorage.getItem("favs")),
      filtrar_por: "",
      loading: false,
    };
  },
  methods: {
    async cargarpersonajes(data) {
      this.filtrar_por = data;
      this.loading = true;
      setTimeout(() => (this.loading = false), 2000);
      try {
        const response = await axios.get(
          `https://www.breakingbadapi.com/api/characters?name=${this.filtrar_por}`
        );
        this.listaPersonajes = response.data;
      } catch (error) {
        console.log(error);
      }
    },
    anhadir(data) {
      if (!this.listaPersonajesFav.includes(data)) {
        this.listaPersonajesFav.push(data);
        localStorage.setItem("favs", JSON.stringify(this.listaPersonajesFav));
      }
    },
    eliminarPersonaje(data) {
      this.listaPersonajesFav = this.listaPersonajesFav.filter(
        (el) => el !== data
      );
      localStorage.setItem("favs", JSON.stringify(this.listaPersonajesFav));
    },
  },
  components: { MiLista, MiBuscador, MiListaFav, MiSpinner },
};
</script>

<style scoped></style>
