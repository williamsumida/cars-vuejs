<template>
  <div :key="marca.id" v-for="marca in marcas">
    <MarcaCard
      @delete-marca="$emit('delete-marca', marca.id, marca.nome)"
      :marca="marca"
    ></MarcaCard>
  </div>
</template>

<script>
import MarcaCard from "./MarcaCard";

export default {
  name: "Marcas",
  props: {
    marcas: Array,
  },
  components: {
    MarcaCard,
  },
  emits: ["delete-marca"],
};
</script>
