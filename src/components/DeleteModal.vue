<template>
  <div class="modal-delete">
    <div>
      <h1 class="modal-title">Excluir contato</h1>
      <hr />
    </div>
    <div class="modal-text">Deseja realmente excluir o contato?</div>
    <hr />
    <div class="cancel-buttons">
      <a class="modal-cancel" @click="$emit('close')">Cancelar </a>
      <button
        type="button"
        class="modal-save"
        @click="$emit('handleContact', { operation }), $emit('close')"
      >
        <span>Excluir</span>
      </button>
    </div>
  </div>
</template>

<script setup>
import { defineEmits } from "vue";

defineEmits(["close", "handleContact"]);
</script>

<script>
export default {
  props: {
    operation: String,
  },
};
</script>

<style scoped>
.modal-text {
  padding: 1rem 0 2.8rem 1.5rem;
  font-size: 0.875rem;
}

.modal > div {
  width: 27rem;
  height: 12.9rem;
}
</style>