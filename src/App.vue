<template>
  <div class="container">
    <h1 class="titulo">Carros</h1>
    <button @click="toggleModalCarro">Criar Carro</button>
    <form @submit="onFilterCarro" class="container-filtro">
      <label class="label-filtro-esquerda">Nome</label>
      <input
        class="input-filtro-esquerda"
        type="text"
        v-model="nome_carro"
        name="nome"
        placeholder="Nome do carro"
      />
      <label class="label-filtro-direita">Origem</label>
      <input
        class="input-filtro-direita"
        type="text"
        v-model="origem_carro"
        name="origem"
        placeholder="Origem do carro"
      />
      <button
        type="button"
        @click="onFilterCarro(nome_carro, origem_carro)"
        class="btn-filtro"
      >
        filtrar
      </button>
    </form>
    <Modal @close="toggleModalCarro" :modalActive="modalActiveCarro">
      <CriarCarro @close="toggleModal" :modalActive="modalActiveCarro" />
    </Modal>
    <Carros @delete-carro="deleteCarro" :carros="carros" />

    <h1 class="titulo">Marcas</h1>
    <button @click="toggleModalMarca">Criar Marca</button>
    <form @submit="onFilterMarca" class="container-filtro">
      <label class="label-filtro-esquerda">Nome</label>
      <input
        class="input-filtro-esquerda"
        type="text"
        v-model="nome_marca"
        name="nome"
        placeholder="Nome da marca"
      />
      <label class="label-filtro-direita">Origem</label>
      <input
        class="input-filtro-direita"
        type="text"
        v-model="origem_marca"
        name="origem"
        placeholder="Origem da marca"
      />
      <button
        type="button"
        @click="onFilterMarca(nome_marca, origem_marca)"
        class="btn-filtro"
      >
        filtrar
      </button>
    </form>

    <Modal @close="toggleModalMarca" :modalActive="modalActiveMarca">
      <CriarMarca @close="toggleModalMarca" :modalActive="modalActiveMarca" />
    </Modal>
    <Marcas @delete-marca="deleteMarca" :marcas="marcas" />
  </div>
</template>

<script>
import axios from "axios";
import Carros from "./components/Carros";
import Marcas from "./components/Marcas";
import Modal from "./components/Modal";
import CriarCarro from "./components/CriarCarro";
import CriarMarca from "./components/CriarMarca";
import { ref } from "vue";

export default {
  name: "App",
  components: {
    Carros,
    Marcas,
    Modal,
    CriarCarro,
    CriarMarca,
  },
  setup() {
    const modalActiveCarro = ref(false);
    const modalActiveMarca = ref(false);
    const toggleModalCarro = () => {
      modalActiveCarro.value = !modalActiveCarro.value;
    };
    const toggleModalMarca = () => {
      modalActiveMarca.value = !modalActiveMarca.value;
    };
    return {
      modalActiveCarro,
      toggleModalCarro,
      modalActiveMarca,
      toggleModalMarca,
    };
  },
  data() {
    return {
      carros: [],
      marcas: [],
    };
  },
  methods: {
    deleteCarro(id, nome) {
      if (confirm(`Deseja deletar ${nome}?`)) {
        axios.delete(`http://localhost:8000/carro/${id}`);
        axios
          .get("http://localhost:8000/carro")
          .then((response) => (this.carros = response.data));
        location.reload();
      }
    },
    deleteMarca(id, nome) {
      if (confirm(`Deseja deletar ${nome}?`)) {
        axios.delete(`http://localhost:8000/marca/${id}`);
        axios
          .get("http://localhost:8000/marca")
          .then((response) => (this.marca = response.data));
        location.reload();
      }
    },
    onFilterCarro(nome_carro, origem_carro) {
      console.log(nome_carro);
      console.log(origem_carro);
      axios
        .get("http://localhost:8000/carro", {
          params: { nome: nome_carro, origem: origem_carro },
        })
        .then((response) => (this.carros = response.data));
    },
    onFilterMarca(nome_marca, origem_marca) {
      axios
        .get("http://localhost:8000/marca", {
          params: { nome: nome_marca, origem: origem_marca },
        })
        .then((response) => (this.marcas = response.data));
    },
  },
  mounted() {
    axios
      .get("http://localhost:8000/carro")
      .then((response) => (this.carros = response.data));
    axios
      .get("http://localhost:8000/marca")
      .then((response) => (this.marcas = response.data));
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container-filtro {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-row: 2;
  grid-column: 3;
  text-align: left;
  width: 200px;
  margin-left: auto;
  margin-right: auto;
  align-content: center;
  justify-content: space-around;
  grid-gap: 1px;
  margin-top: 30px;
}

.label-filtro-esquerda {
  grid-column: 1;
  grid-row: 1;
  height: 20px;
}

.input-filtro-esquerda {
  grid-column: 1;
  grid-row: 2;
  height: 15px;
}

.label-filtro-direita {
  grid-column: 2;
  grid-row: 1;
  height: 15px;
}

.input-filtro-direita {
  grid-column: 2;
  grid-row: 2;
  height: 15px;
}

.btn-filtro {
  grid-column: 3;
  grid-row: 2;
  height: 29px;
}

.titulo {
  margin-top: 100px;
}

input {
  padding: 5px;
  margin: 5px;
}
</style>
