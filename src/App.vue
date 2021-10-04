<template>
  <div class="container">
    <h1>Carros</h1>
    <button @click="toggleModalCarro">Criar Carro</button>
    <Modal @close="toggleModalCarro" :modalActive="modalActiveCarro">
      <CriarCarro @close="toggleModal" :modalActive="modalActiveCarro" />
    </Modal>
    <Carros @delete-carro="deleteCarro" :carros="carros" />

    <h1>Marcas</h1>
    <button @click="toggleModalMarca">Criar Marca</button>
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
</style>
