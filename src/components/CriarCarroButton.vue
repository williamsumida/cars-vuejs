<template>
  <button @click="onClick()">Criar Carro</button>
</template>

<script>
export default {
  name: "Button",
  props: {
    carros: Array,
  },
  methods: {
    onClick() {},
  },
};
</script>
