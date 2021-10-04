<template>
  <div class="container">
    <Header />
    <Button @click="toggleModal" :carros="carros" />
    <Modal @close="toggleModal" :modalActive="modalActive">
      <CriarCarro @close="toggleModal" :modalActive="modalActive" />
    </Modal>
    <Carros @delete-carro="deleteCarro" :carros="carros" />
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/Header";
import Button from "./components/CriarCarroButton";
import Carros from "./components/Carros";
import Modal from "./components/Modal";
import CriarCarro from "./components/CriarCarro";
import { ref } from "vue";

export default {
  name: "App",
  components: {
    Header,
    Button,
    Carros,
    Modal,
    CriarCarro,
  },
  setup() {
    const modalActive = ref(false);
    const toggleModal = () => {
      modalActive.value = !modalActive.value;
    };
    return { modalActive, toggleModal };
  },
  data() {
    return {
      carros: [],
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
  },
  mounted() {
    axios
      .get("http://localhost:8000/carro")
      .then((response) => (this.carros = response.data));
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
