<template>
  <div class="contact-list">
    <table>
      <tr class="table-heading">
        <td></td>
        <td>Contatos</td>
        <td>E-mail</td>
        <td>Telefone</td>
        <td></td>
      </tr>
      <transition-group name="highlight">
        <tr
          v-for="(item, i) in filteredList"
          :key="item.id"
          class="table-content"
        >
          <td class="contact-icon">
            <div v-bind:class="'start-with-' + item.name[0]">
              <span>{{ item.name[0] }}</span>
            </div>
          </td>
          <td class="content-td">{{ item.name }}</td>
          <td class="content-td">{{ item.email }}</td>
          <td class="content-td">{{ item.telefone }}</td>
          <td class="table-icons content-td">
            <img
              src="../../public/edit.svg"
              @click="(isOpen = true), setProps(item)"
            /><img
              src="../../public/delete.svg"
              @click="(openDelete = true), setProps(item, i)"
            />
          </td>
        </tr>
      </transition-group>
    </table>
    <div class="modal" v-if="isOpen">
      <ContactModal
        @close="isOpen = false"
        @handle-contact="parentsComunication"
        operation="edit"
        :Pname="name"
        :Pemail="email"
        :Ptelefone="telefone"
      />
    </div>
    <div class="modal" v-if="openDelete">
      <DeleteModal
        @close="openDelete = false"
        @handle-contact="parentsComunication"
        operation="delete"
      />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import ContactModal from "./ContactModal.vue";
import DeleteModal from "./DeleteModal";

export default {
  name: "ContactList",
  props: {
    contacts: Array,
    query: String,
  },
  setup() {
    const isOpen = ref(false);
    const openDelete = ref(false);

    return { isOpen, openDelete };
  },
  components: {
    ContactModal,
    DeleteModal,
  },
  data() {
    return {
      contact: {
        name: "",
        email: "",
        telefone: "",
        id: "",
      },
      myList: [],
    };
  },
  methods: {
    setProps(item) {
      this.name = item.name;
      this.email = item.email;
      this.telefone = item.telefone;
      this.id = item.id;
    },
    parentsComunication(props) {
      const obj = {
        name: props.name,
        email: props.email,
        telefone: props.telefone,
        operation: props.operation,
        id: this.id,
      };
      this.$emit("handleContact", obj);
    },
  },
  computed: {
    filteredList() {
      return this.contacts
        .filter((item) =>
          item.name.toLowerCase().includes(this.query.toLowerCase())
        )
        .sort((a, b) => {
          let fa = a.name.toLowerCase(),
            fb = b.name.toLowerCase();
          if (fa < fb) {
            return -1;
          }
          if (fa > fb) {
            return 1;
          }
          return 0;
        });
    },
  },
};
</script>

<style scoped>
.contact-list {
  padding-top: 36px;
}

table {
  width: 100%;
  background-color: #fff;
  border: 1px solid #e1e1e1;
  border-radius: 4px;
  border-spacing: 0;
}

.table-heading {
  width: 100%;
  color: #9198af;
}

.table-heading td {
  padding-top: 16px;
  padding-bottom: 9px;
}

.content-td {
  border-top: 1px solid #e1e1e1;
  padding-top: 12px;
  padding-bottom: 12px;
  color: #2a2d3b;
}

.table-content {
  width: 100%;
}

.table-content:hover {
  background-color: #fff3f2;
  transition: 0.3s;
}

.table-icons {
  padding-right: 16px;
  text-align: right;
}

.table-icons img:hover {
  cursor: pointer;
}

.table-icons img {
  margin-left: 24px;
}

.contact-icon {
  text-align: center;
  border-top: 1px solid #e1e1e1;
  width: 3rem;
}

.contact-icon div {
  margin-left: 0.5rem;
  width: 1.5rem;
  height: 1.5rem;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 100%;
}

.contact-icon span {
  color: white;
}

.highlight-move, /* apply transition to moving elements */
.highlight-enter-active {
  transition: all 0.5s ease;
  animation: tensecondshighlight 10s;
}

.highlight-enter-active,
.highlight-leave-active {
  transition: opacity 0.5s ease;
}

.highlight-enter-from,
.highlight-leave-to {
  opacity: 0;
}

@keyframes tensecondshighlight {
  0%,
  100% {
    background: #fff3f2;
  }
}
</style>