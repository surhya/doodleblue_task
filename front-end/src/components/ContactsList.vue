<template>
  <div class="contacts-list">
    <div class="data">
      <table class="ui celled table">
        <thead>
          <tr>
            <th style="width: 50px; text-align: center;">ID</th>
            <th>Name</th>
            <th>Phone No</th>
            <th>E-mail</th>
            <th style="width: 148px;">Action</th>
          </tr>
        </thead>

        <tbody>
          <Contacts
            v-for="contacts in contacts"
            :key="contacts.id"
            :contacts="contacts"
            @onDelete="onDelete"
            @onEdit="onEdit"
          />
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import Contacts from "./Contacts";
export default {
  name: "ContactsList",
  components: {
    Contacts
  },
  props: {
    contacts: {
      type: Array
    }
  },
  methods: {
    onDelete(id) {
      
      this.$emit("onDelete", id);
    },
    onEdit(data) {
      
      this.$emit("onEdit", data);
    }
  }
};
</script>

<style scoped></style>
