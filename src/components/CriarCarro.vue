<template>
  <div class="container">
    <h1>Criar Carro</h1>
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
        <label>Kilometragem por galão</label>
        <input
          type="text"
          v-model="km_por_galao"
          name="km_por_galao"
          placeholder="km/galão"
        />
      </div>
      <div>
        <label>Cilindros</label>
        <input
          type="text"
          v-model="cilindros"
          name="cilindros"
          placeholder="Cilindros"
        />
      </div>
      <div>
        <label>Cavalos de força</label>
        <input
          type="text"
          v-model="cavalos_de_forca"
          name="cavalos_de_forca"
          placeholder="Cavalos de força"
        />
      </div>
      <div>
        <label>Peso</label>
        <input
          type="text"
          v-model="peso"
          name="peso"
          placeholder="Peso do carro"
        />
      </div>
      <div>
        <label>Aceleração</label>
        <input
          type="text"
          v-model="aceleracao"
          name="aceleracao"
          placeholder="Aceleração do carro"
        />
      </div>
      <div>
        <label>Ano</label>
        <input
          type="text"
          v-model="ano"
          name="ano"
          placeholder="Ano do carro"
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
      <button
        type="button"
        @click="
          close(
            nome,
            km_por_galao,
            aceleracao,
            peso,
            cavalos_de_forca,
            cilindros,
            ano,
            origem
          )
        "
      >
        Salvar
      </button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      nome: "",
      km_por_galao: "",
      aceleracao: "",
      peso: "",
      cavalos_de_forca: "",
      cilindros: "",
      ano: "",
      origem: "",
    };
  },
  props: ["modalActive"],
  setup(props, { emit }) {
    const close = (
      nome,
      km_por_galao,
      aceleracao,
      peso,
      cavalos_de_forca,
      cilindros,
      ano,
      origem
    ) => {
      emit("close");
      axios.post("http://localhost:8000/carro", {
        nome,
        km_por_galao,
        aceleracao,
        peso,
        cavalos_de_forca,
        cilindros,
        ano,
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
