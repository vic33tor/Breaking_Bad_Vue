<template>
  <div class="flex flex-col my-auto items-center">
    <input
      v-model="buscador"
      class="bg-[#F0EBCE] w-64 h-8 border-2 border-[#AA8B56]"
      placeholder="Busca un personaje"
      @keydown.enter="enviaEntrada"
    />
  </div>
</template>

<script>
export default {
  name: "MiBuscador",
  emits: ["enviaRespuesta"],
  data() {
    return {
      buscador: "",
    };
  },
  methods: {
    enviaEntrada() {
      this.$emit("enviaRespuesta", this.buscador);
    },
  },
};
</script>

<style scoped></style>
