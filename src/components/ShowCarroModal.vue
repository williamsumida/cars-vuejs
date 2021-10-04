<template>
  <transition name="modal-animation">
    <div v-show="modalActive" class="modal">
      <transition name="modal-animation-inner">
        <div v-show="modalActive" class="modal-inner">
          <i class="fas fa-times"></i>
          <slot />
        </div>
        <button>Fechar</button>
      </transition>
    </div>
  </transition>
</template>

<script>
export default {
  props: ["modalActive"],
};
</script>

<style></style>
