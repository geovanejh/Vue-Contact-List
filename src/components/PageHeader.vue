<template>
  <div class="header">
    <img class="logo" src="../../public/ubook.svg" />
    <a class="btn-open-modal" v-show="contacts.length" @click="isOpen = true">
      <img src="../../public/plus.svg" />
      <span class="create-contact"> Criar contato </span>
    </a>
    <div class="modal" v-if="isOpen">
      <ContactModal
        @close="isOpen = false"
        @handle-contact="parentsComunication"
        operation="add"
      />
    </div>
    <div class="search-field">
      <input
        type="text"
        class="search-input"
        placeholder="Buscar..."
        v-model="query"
        @keyup="$emit('queryChange', query)"
      />
      <img class="search-logo" src="../../public/search.svg" />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import ContactModal from "./ContactModal.vue";

export default {
  name: "PageHeader",
  setup() {
    const isOpen = ref(false);

    return { isOpen };
  },
  data() {
    return {
      query: "",
    };
  },
  props: {
    contacts: Array,
  },
  components: {
    ContactModal,
  },
  methods: {
    parentsComunication(props) {
      const obj = {
        name: props.name,
        email: props.email,
        telefone: props.telefone,
        operation: props.operation,
      };
      this.$emit("handleContact", obj);
      this.isOpen = false;
    },
  },
  emits: ["handleContact", "queryChange"],
};
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.create-contact {
  height: 16px;
  margin: 0 0 0 8px;
  font-size: 0.875rem;
  color: #fa7268;
  font-weight: 600;
}

.logo {
  height: 2rem;
  width: auto;
}

.search-field {
  width: 70vw;
  height: 2rem;
  padding: 7px 8px 6px;
  border-radius: 4px;
  background-color: #e4e7f4;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.search-input {
  width: 100%;
  color: #9198af;
  background-color: transparent;
  border: none;
  height: 19px;
  font-size: 16px;
  font-weight: normal;
  font-stretch: normal;
  font-style: normal;
  line-height: normal;
  letter-spacing: normal;
}

.search-input:focus {
  outline: none;
}

.search-logo {
  margin-right: 8px;
}

.btn-open-modal {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 2rem;
  padding: 8px 22px 8px 16px;
  border-radius: 20px;
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.16),
    0 0 0 0.5px rgba(0, 0, 0, 0.08), inset 0 0 0 0.5px rgba(0, 0, 0, 0.08),
    0 2px 4px 0.5px rgba(0, 0, 0, 0.16);
  background-color: #dbff90;
}

.btn-open-modal:hover {
  cursor: pointer;
}
</style>