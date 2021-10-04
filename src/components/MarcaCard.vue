<template>
  <Modal @close="toggleModal" :modalActive="modalActive">
    <AcessarMarca
      @close="toggleModal"
      :modalActive="modalActive"
      :marca="marca"
    />
  </Modal>
  <div @dblclick="acessarMarca()" class="marca">
    <p
      @click="$emit('delete-marca', marca.id, marca.nome)"
      class="fas fa-times"
    ></p>
    <p>Nome: {{ marca.nome }}</p>
    <p>Origem: {{ marca.origem }}</p>
  </div>
</template>

<script>
import Modal from "./Modal";
import AcessarMarca from "./AcessarMarca";
import { ref } from "vue";
export default {
  name: "CarroCard",
  components: { Modal, AcessarMarca },
  setup() {
    const modalActive = ref(false);
    const toggleModal = () => {
      modalActive.value = !modalActive.value;
    };
    return { modalActive, toggleModal };
  },
  props: {
    marca: Object,
  },
  methods: {
    acessarMarca() {
      this.toggleModal();
    },
  },
};
</script>
<style scope>
.marca {
  height: auto;
  width: 250px;
  background: #fff;
  box-shadow: 0 0 20px 8px #d0d0d0;
  border-radius: 10px;
  cursor: pointer;

  text-align: left;
  overflow: hidden;

  padding: 20px;

  margin-top: 30px;
  margin-left: auto;
  margin-right: auto;

  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.fas {
  color: red;
  float: right;
}
</style>
