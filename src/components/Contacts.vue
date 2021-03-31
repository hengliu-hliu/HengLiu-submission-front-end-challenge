<template>
  <div class="contacts">
    <h1>{{ msg }}</h1>

    <p class="flex-container">
      To add a contact, please enter their name and phone number
    </p>

    <form
      class="flex-container"
      @submit.prevent="recordContact"
      autocomplete="off"
    >
      <input
        class="form-input"
        type="text"
        v-model="name"
        placeholder="name"
        maxlength="30"
        required
      />

      <input
        class="form-input"
        type="text"
        v-model="phone"
        placeholder="123-456-7890"
        pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
        oninvalid="setCustomValidity('Field Required. This format required: 123-456-7890')"
        oninput="setCustomValidity('')"
        maxlength="12"
        required
      />

      <button class="button1" type="submit" v:on:keyup.enter>
        +
      </button>
    </form>

    <h3>Current Contacts</h3>

    <li class="flex-container2">
      <b><div class="flex-div">Name</div></b>
      <b><div class="flex-div">Phone Number</div></b>
    </li>

    <div v-for="(contact, index) in contacts" :key="contact.id">
      <li class="flex-container2">
        <div class="flex-div">{{ contact.name }}</div>
        <div class="flex-div">{{ contact.phone }}</div>

        <button class="button2" value="-" v-on:click="removeContact(index)">
          -
        </button>
      </li>
      <br />
    </div>
  </div>
</template>

<script>
export default {
  name: "Contacts",
  props: {
    msg: String,
  },
  data() {
    return {
      name: null,
      phone: null,
      contacts: JSON.parse(localStorage.getItem("contacts")),
    };
  },
  methods: {
    recordContact: function() {
      // checks if contacts is null,
      if (!this.contacts) {
        this.contacts = [];
      }

      // pushes current name and phone to end of contacts array
      this.contacts.push({
        name: this.name,
        phone: this.phone,
      });

      // sets "contacts" localstorage to current contacts array
      localStorage.setItem("contacts", JSON.stringify(this.contacts));

      //resets form
      this.name = "";
      this.phone = "";
    },
    // removes contact entry
    removeContact: function(index) {
      this.contacts.splice(index, 1);
      localStorage.setItem("contacts", JSON.stringify(this.contacts));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}

.flex-container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.form-input {
  padding: 10px 10px;
  border-radius: 5px;
  border-style: solid;
  border-color: #008cba;
  margin: 5px;
  width: 150px;
}

.button1 {
  background-color: #008cba;
  color: #ffffff;
  border-radius: 5px;
  padding: 10px 20px;
  border: none;
  margin: 5px;
}

.flex-container2 {
  display: flex;
  justify-content: center;
  align-content: center;
  align-items: center;
}

.flex-div {
  padding: 10px 5px;
  margin: 5px;
  width: 250px;
}

.button2 {
  background-color: #f4000c;
  color: #ffffff;
  border-radius: 3px;
  padding: 1px 4px;
  border: none;
  align-items: center;
  width: 25px;
  height: 19px;
  min-width: none;
}
</style>
