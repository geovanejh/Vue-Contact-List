<template>
  <div class="modal-content">
    <h1 v-show="operation === 'add'" class="modal-title">Criar novo contato</h1>
    <h1 v-show="operation === 'edit'" class="modal-title">Editar contato</h1>
    <hr />
    <div class="modal-form">
      <label for="addName">Nome</label>
      <input type="text" class="modal-input-full" id="addName" v-model="name" />
      <label for="addEmail">E-mail</label>
      <input
        type="text"
        class="modal-input-full"
        id="addEmail"
        v-model="email"
      />
      <label for="addTelefone">Telefone</label>
      <input
        type="text"
        class="modal-input-half"
        id="addTelefone"
        v-model="telefone"
      />
    </div>
    <hr />
    <div class="cancel-buttons">
      <a class="modal-cancel" @click="$emit('close')">Cancelar </a>
      <button
        v-if="name.length === 0 && email.length === 0 && telefone.length === 0"
        type="button"
        disabled
        class="modal-save"
      >
        <span>Salvar</span>
      </button>
      <button
        v-else
        type="submit"
        class="modal-save"
        @click="
          $emit('handleContact', { name, email, telefone, operation }),
            $emit('close')
        "
      >
        <span>Salvar</span>
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
  mounted() {
    if (this.Pname) {
      this.name = this.Pname;
      this.email = this.Pemail;
      this.telefone = this.Ptelefone;
    }
  },
  data() {
    return {
      name: "",
      email: "",
      telefone: "",
    };
  },
  props: {
    operation: String,
    Pname: String,
    Pemail: String,
    Ptelefone: String,
  },
};
</script>

<style>
.root {
  position: relative;
}

.modal {
  position: absolute;
  top: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.4);
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 16px 10px 0 rgba(0, 0, 0, 0.16);
}

.modal > div {
  background-color: #fff;
  width: 432px;
  height: 342px;
  border-radius: 10px;
}

.modal-title {
  padding: 10px 0 8px 16px;
  font-size: 16px;
  font-weight: normal;
}

.modal-form {
  padding: 8px 24px 0 24px;
  font-size: 14px;
}

hr {
  width: 100%;
  height: 1px;
  background-color: #c0c3d2;
  border: 0;
}

.modal-input-full {
  margin-top: 4px;
  width: 100%;
  padding: 9px 0 7px 5px;
  border-radius: 4px;
  border: solid 1px #c0c3d2;
  margin-bottom: 16px;
}

.modal-input-half {
  margin-top: 4px;
  width: 33%;
  padding: 9px 0 7px 5px;
  border-radius: 4px;
  border: solid 1px #c0c3d2;
  margin-bottom: 16px;
}

label {
  display: block;
}

.modal-cancel {
  width: 56px;
  height: 16px;
  right: 0;
  font-size: 14px;
  color: #fa7268;
  margin-right: 16px;
}

.modal-cancel:hover {
  cursor: pointer;
}

.modal-save {
  margin-right: 24px;
  padding: 7px 14px;
  border-radius: 16px;
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.16),
    0 0 0 0.5px rgba(0, 0, 0, 0.08), inset 0 0 0 0.5px rgba(0, 0, 0, 0.08),
    0 2px 4px 0.5px rgba(0, 0, 0, 0.16);
  background-color: #fa7268;
  border: 0;
}

.modal-save:disabled {
  opacity: 0.32;
}

.modal-save span {
  width: 40px;
  height: 16px;
  font-family: Roboto;
  font-size: 14px;
  font-weight: 500;
  font-stretch: normal;
  font-style: normal;
  line-height: normal;
  letter-spacing: normal;
  text-align: center;
  color: #fff;
}

.modal-save:hover {
  cursor: pointer;
}

.cancel-buttons {
  display: flex;
  justify-content: end;
  align-items: center;
}

.btn-open-modal {
  display: flex;
  border: 0;
  justify-content: center;
  align-items: center;
  height: 40px;
  padding: 8px 22px 8px 16px;
  border-radius: 20px;
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.16),
    0 0 0 0.5px rgba(0, 0, 0, 0.08), inset 0 0 0 0.5px rgba(0, 0, 0, 0.08),
    0 2px 4px 0.5px rgba(0, 0, 0, 0.16);
  background-color: #dbff90;
}
</style>