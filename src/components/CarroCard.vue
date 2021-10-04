<template>
  <Modal @close="toggleModal" :modalActive="modalActive">
    <AcessarCarro
      @close="toggleModal"
      :modalActive="modalActive"
      :carro="carro"
    />
  </Modal>
  <div @dblclick="acessarCarro()" class="carro">
    <p
      @click="$emit('delete-carro', carro.id, carro.nome)"
      class="fas fa-times"
    ></p>
    <p>Nome: {{ carro.nome }}</p>
    <p>Origem: {{ carro.origem }}</p>
    <p>Ano: {{ carro.ano }}</p>
  </div>
</template>

<script>
import Modal from "./Modal";
import AcessarCarro from "./AcessarCarro";
import { ref } from "vue";
export default {
  name: "CarroCard",
  components: { Modal, AcessarCarro },
  setup() {
    const modalActive = ref(false);
    const toggleModal = () => {
      modalActive.value = !modalActive.value;
    };
    return { modalActive, toggleModal };
  },
  props: {
    carro: Object,
  },
  methods: {
    acessarCarro() {
      this.toggleModal();
    },
  },
};
</script>
<style scope>
.carro {
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
