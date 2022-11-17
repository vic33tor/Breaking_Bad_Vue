<template>
  <div
    class="bg-[#F0EBCE] text-xl flex justify-center items-center w-52 h-10 m-auto mt-2 text-[#395144] border-2 border-[#AA8B56]"
  >
    <h1>Lista de busquedas</h1>
  </div>
  <div
    v-if="this.lista.length == 0"
    class="text-xl flex justify-center items-center m-auto mt-2 text-[#F0EBCE]"
  >
    Ninguna busqueda registrada
  </div>
  <div v-else>
    <ul>
      <li v-for="(el, idx) in this.lista" :key="idx">
        <MiPersonaje :elemento="el" @aFavs="enviarFavs" />
      </li>
    </ul>
  </div>
</template>

<script>
import MiPersonaje from "@/components/MiPersonaje.vue";

export default {
  name: "MiLista",
  props: {
    lista: {
      type: Array,
    },
  },
  emits: ["aFavs"],
  methods: {
    enviarFavs(data) {
      this.$emit("aFavs", data);
    },
  },
  components: { MiPersonaje },
};
</script>

<style scoped></style>
