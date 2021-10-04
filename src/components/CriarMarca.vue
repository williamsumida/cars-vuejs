<template>
  <div class="container">
    <h1>Criar Marca</h1>
    <form @submit="onSubmit">
      <div>
        <label>Nome</label>
        <input
          type="text"
          v-model="nome"
          name="nome"
          placeholder="Nome do carro"
        />
      </div>
      <div>
        <label>Origem</label>
        <input
          type="text"
          v-model="origem"
          name="origem"
          placeholder="Origem do carro"
        />
      </div>
      <button type="button" @click="close(nome, origem)">Salvar</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      nome: "",
      origem: "",
    };
  },
  props: ["modalActive"],
  setup(props, { emit }) {
    const close = (nome, origem) => {
      emit("close");
      axios.post("http://localhost:8000/marca", {
        nome,
        origem,
      });
      location.reload();
    };
    return { close };
  },
};
</script>
<style scoped>
.container {
  background-color: aliceblue;
  display: block;
  padding: 20px;
}
div {
  padding: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
input {
  padding: 5px;
  margin: 5px;
}
button {
  padding: 20px 30px;
  border: none;
  font-size: 16px;
  background-color: #006ff7;
  color: #fff;
  cursor: pointer;
  border-radius: 10px;
}
</style>
