<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />

    <PropsVue msg="Welcome to Your Vue.js App" :values="values" />
  </div>
</template>

<script>
import PropsVue from "./components/PropsVue";

export default {
  name: "App",

  components: {
    PropsVue
  },

  data() {
    return {
      values: {
        min: 0,
        max: 10,
        low: 3,
        high: 5,
        optimum: 6,
        value: 7
      }
    };
  }
};
</script>

<style>
body {
  background-color: #2c3e50;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: azure;
  margin-top: 60px;
}
</style>


