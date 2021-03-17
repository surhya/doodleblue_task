<template>
  <tr>
    <td>{{ contacts.id }}</td>
    <td>{{ contacts.name }}</td>
    <td>{{ contacts.phone_no }}</td>
    <td>{{ contacts.email }}</td>
    <td>
      <button class="mini ui blue button" @click="onEdit">Edit</button>
      <button class="mini ui red button" @click="onDelete">Delete</button>
    </td>
  </tr>
</template>

<script>
export default {
  name: "Contacts",
  props: {
    contacts: {
      type: Object
    }
  },
  methods: {
    onDelete() {
     
      this.$emit("onDelete", this.contacts.id);
    },
    onEdit() {
    
      this.$emit("onEdit", this.contacts);
    }
  }
};
</script>

<style scoped></style>
