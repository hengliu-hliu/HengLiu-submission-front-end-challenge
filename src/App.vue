<template>
  <div id="app">
    <Contacts msg="Welcome to Your Contacts" />
  </div>
</template>

<script>
import Contacts from "./components/Contacts.vue";

export default {
  name: "App",
  components: {
    Contacts,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}
</style>
