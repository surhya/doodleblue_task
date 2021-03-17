<template>
  <div id="app">
    <div class="ui fixed inverted menu vue-color">
      <div class="ui container">
        <a href="#" class="header item">CONTACTS</a>
      </div>
    </div>

    <div class="ui main container">
      <MyForm :form="form" @onFormSubmit="onFormSubmit" />
      <Loader v-if="loader" />
      <ContactsList
        :contacts="contacts"
        @onDelete="onDelete"
        @onEdit="onEdit"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import MyForm from "./components/MyForm";
import ContactsList from "./components/ContactsList";
import Loader from "./components/Loader";

export default {
  name: "App",
  components: {
    MyForm,
    ContactsList,
    Loader
  },
  data() {
    return {
      url: "http://localhost/api/contacts",
      contacts: [],
      form: { name: "", phone_no: "", email: "", isEdit: false },
      loader: false
    };
  },
  methods: {
    getContacts() {
      this.loader = true;

      axios.get(this.url).then(data => {
        this.contacts = data.data;
        this.loader = false;
      });
    },
    deleteContacts(id) {
      this.loader = true;

      axios
        .delete(`${this.url}/${id}`)
        .then(() => {
          this.getContacts();
        })
        .catch(e => {
          alert(e);
        });
    },
    createContacts(data) {
      this.loader = true;

      axios
        .post(this.url, {
          name: data.name,
          phone_no: data.phone_no,
          email: data.email
        })
        .then(() => {
          this.getContacts();
        })
        .catch(e => {
          alert(e);
        });
    },
    editContacts(data) {
      this.loader = true;

      axios
        .put(`${this.url}/${data.id}`, {
          name: data.name,
          phone_no: data.phone_no,
          email: data.email
        })
        .then(() => {
          this.getContacts();
        })
        .catch(e => {
          alert(e);
        });
    },
    onDelete(id) {
     

      this.deleteContacts(id);
    },
    onEdit(data) {
      this.form = data;
      this.form.isEdit = true;
    },
    onFormSubmit(data) {
    
      if (data.isEdit) {
      
        this.editContacts(data);
      } else {
      
        this.createContacts(data);
      }
    }
  },
  created() {
    this.getContacts();
  }
};
</script>

<style>
.vue-color {
  background: #41b883 !important;
}

.main.container {
  margin-top: 60px;
}

.submit-button {
  margin-top: 24px !important;
  float: right;
}

.data {
  margin-top: 15px;
}

thead tr th {
  background: #e0e0e0 !important;
}

.ui.inverted.dimmer {
  background-color: rgba(255, 255, 255, 0) !important;
}
</style>
