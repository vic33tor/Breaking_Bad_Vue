<template>
  <div
    class="bg-[#F0EBCE] text-xl flex justify-center items-center w-52 h-10 m-auto mt-2 text-[#395144] border-2 border-[#AA8B56]"
  >
    <h1>Lista favoritos</h1>
  </div>
  <div
    v-if="this.lista.length == 0"
    class="text-xl flex justify-center items-center m-auto mt-2 text-[#F0EBCE]"
  >
    Ningún personaje en favoritos
  </div>
  <div v-else>
    <ul>
      <li v-for="(el, idx) in this.lista" :key="idx">
        <MiPersonajefav :elemento="el" @eliminar="eliminarPersonaje" />
      </li>
    </ul>
  </div>
</template>

<script>
import MiPersonajefav from "./MiPersonajefav.vue";

export default {
  name: "MiListaFav",
  props: {
    lista: {
      type: Array,
    },
  },
  emits: ["eliminar"],
  methods: {
    eliminarPersonaje(data) {
      this.$emit("eliminar", data);
    },
  },
  components: { MiPersonajefav },
};
</script>

<style scoped></style>
