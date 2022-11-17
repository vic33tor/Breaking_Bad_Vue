<template>
  <div
    class="grid grid-cols-2 max-w-sm mx-auto p-6 bg-[#F0EBCE] rounded-lg shadow-xl mt-3 border-2 border-[#AA8B56]"
  >
    <div>
      <img class="h-38 w-38" :src="elemento.img" />
    </div>
    <div class="ml-6 pt-1">
      <h4 class="text-xl font-bold text-[#4E6C50] leading-tight">
        {{ elemento.name }}
      </h4>
      <div v-if="masInformacion">
        <p class="text-base text-gray-900 leading-normal">Occupation:</p>
        <p
          v-for="(el, idx) in elemento.occupation"
          :key="idx"
          class="text-base text-gray-600 leading-normal"
        >
          {{ "-" + el }}
        </p>
        <p class="text-base text-gray-900 leading-normal">Status:</p>
        <p class="text-base text-gray-600 leading-normal">
          {{ elemento.status }}
        </p>
        <p class="text-base text-gray-900 leading-normal">Nickname:</p>
        <p class="text-base text-gray-600 leading-normal">
          {{ elemento.nickname }}
        </p>
        <p class="text-base text-gray-900 leading-normal">Portrayed:</p>
        <p class="text-base text-gray-600 leading-normal">
          {{ elemento.portrayed }}
        </p>
      </div>
    </div>
    <div class="grid grid-cols-2 pt-2">
      <div class="h-12 w-20 m-auto pt-4">
        <button
          @click="mostrarInfo"
          class="p-1 bg-[#4E6C50] hover:bg-[#395144] text-white font-bold border border-white rounded"
        >
          {{ textoBotonInfo }}
        </button>
      </div>
      <div class="h-12 w-20 m-auto pt-4">
        <button
          @click="eliminarPersonaje"
          class="p-1 bg-[#4E6C50] hover:bg-[#395144] text-white font-bold border border-white rounded"
        >
          eliminar
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "MiPersonajefav",
  data() {
    return {
      masInformacion: false,
      textoBotonInfo: "mas info",
    };
  },
  props: {
    elemento: {
      type: Object,
      required: true,
    },
  },
  emits: ["eliminar"],
  methods: {
    eliminarPersonaje() {
      if (confirm(`¿Estás seguro de eliminar a ${this.elemento.name}?`))
        this.$emit("eliminar", this.elemento);
    },
    mostrarInfo() {
      if (this.masInformacion == true) {
        this.masInformacion = false;
        this.textoBotonInfo = "mas info";
      } else {
        this.masInformacion = true;
        this.textoBotonInfo = "volver";
      }
    },
  },
};
</script>

<style scoped></style>
