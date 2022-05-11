<template>
  <div>
    <PageHeader
      :contacts="contacts"
      @handle-contact="handleContact"
      @query-change="setQuery"
    />
    <EmptyPageBook
      v-show="contacts.length === 0"
      @handle-contact="handleContact"
    />
    <ContactList
      v-show="contacts.length > 0"
      :contacts="contacts"
      :query="query"
      @handle-contact="handleContact"
    />
  </div>
</template>

<script>
import PageHeader from "./components/PageHeader.vue";
import EmptyPageBook from "./components/EmptyPageBook.vue";
import ContactList from "./components/ContactList.vue";

export default {
  name: "App",
  components: {
    PageHeader,
    EmptyPageBook,
    ContactList,
  },
  data() {
    return {
      contacts: [],
      query: "",
      idCounter: 0,
    };
  },
  methods: {
    handleContact(props) {
      const id = this.contacts.findIndex((x) => x.id === props.id);
      console.log("id", id);
      if (props.operation === "edit") {
        this.contacts[id].name = props.name;
        this.contacts[id].email = props.email;
        this.contacts[id].telefone = props.telefone;
      } else if (props.operation === "add") {
        this.contacts.push({
          name: props.name,
          email: props.email,
          telefone: props.telefone,
          id: this.idCounter++,
        });
      } else if (props.operation === "delete") {
        this.contacts.splice(id, 1);
      }
    },
    setQuery(props) {
      console.log(props);
      this.query = props;
    },
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 16px;
  background-color: #f8f9fd;
  font-family: Roboto;
}

@font-face {
  font-family: Roboto;
  src: url("../public/Roboto.ttf");
}
</style>
