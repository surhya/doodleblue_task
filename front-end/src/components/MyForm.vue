<template>
  <div class="my-form">
    <form class="ui form">
      <div class="fields">
        <div class="four wide field">
          <label>Name</label>
          <input
            type="text"
            name="name"
            placeholder="Name"
            @change="handleChange"
            :value="form.name"
          />
        </div>

        <div class="four wide field">
          <label>Phone No</label>
          <input
            type="text"
            name="phone_no"
            placeholder="Phone No"
            @change="handleChange"
            :value="form.phone_no"
          />
        </div>

        <div class="six wide field">
          <label>E-mail</label>
          <input
            type="email"
            name="email"
            placeholder="joe@gmail.com"
            @change="handleChange"
            :value="form.email"
          />
        </div>

        <div class="two wide field">
          <button :class="btnClass" @click="onFormSubmit">
            {{ btnName }}
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "MyForm",
  data() {
    return {
      btnName: "Save",
      btnClass: "ui primary button submit-button"
    };
  },
  props: {
    form: {
      type: Object
    }
  },
  methods: {
    handleChange(event) {
      const { name, value } = event.target;
      let form = this.form;
      form[name] = value;
      this.form = form;
    },
    onFormSubmit(event) {
      
      event.preventDefault();

      // form validation
      if (this.formValidation()) {
      
        this.$emit("onFormSubmit", this.form);

        this.btnName = "Save";
        this.btnClass = "ui primary button submit-button";

        this.clearFormFields();
      }
    },
    formValidation() {
   
      if (document.getElementsByName("name")[0].value === "") {
        alert("Enter name");
        return false;
      }

      if (document.getElementsByName("phone_no")[0].value === "") {
        alert("Enter phone no");
        return false;
      }

  
      if (document.getElementsByName("email")[0].value === "") {
        alert("Enter email");
        return false;
      }

      return true;
    },
    clearFormFields() {
      // clear form data
      this.form.name = "";
      this.form.phone_no = "";
      this.form.email = "";
      this.form.isEdit = false;
      // clear form fields
      document.querySelector(".form").reset();
    }
  },
  updated() {
    if (this.form.isEdit) {
      this.btnName = "Update";
      this.btnClass = "ui orange button submit-button";
    }
  }
};
</script>

<style></style>
