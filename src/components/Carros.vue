<template>
  <div :key="carro.id" v-for="carro in carros">
    <CarroCard
      @delete-carro="$emit('delete-carro', carro.id, carro.nome)"
      :carro="carro"
    ></CarroCard>
  </div>
</template>

<script>
import CarroCard from "./CarroCard.vue";

export default {
  name: "Carros",
  props: {
    carros: Array,
  },
  components: {
    CarroCard,
  },
  emits: ["delete-carro"],
};
</script>
