<template>
  <div class="book-page">
    <img src="../../public/book.svg" class="book-img" />
    <p>Nenhum contato foi criado ainda.</p>
    <button class="btn-open-modal" @click="isOpen = true">
      <img src="../../public/plus.svg" />
      <span class="create-contact"> Criar contato </span>
    </button>
    <div class="modal" v-if="isOpen">
      <ContactModal
        @close="isOpen = false"
        @handle-contact="parentsComunication"
        operation="add"
      />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import ContactModal from "./ContactModal.vue";
export default {
  name: "EmptyPageBook",
  setup() {
    const isOpen = ref(false);
    return { isOpen };
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
  components: {
    ContactModal,
  },
  emits: ["handleContact"],
};
</script>

<style scoped>
.book-page {
  padding-top: 15vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.book-img {
  height: 337px;
  width: auto;
}

.create-contact {
  height: 16px;
  margin: 0 0 0 8px;
  font-size: 14px;
  font-weight: 500;
  font-stretch: normal;
  font-style: normal;
  line-height: normal;
  letter-spacing: normal;
  color: #fa7268;
}
</style>