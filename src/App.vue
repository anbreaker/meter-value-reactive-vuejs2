<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />

    <MeterComponet :meterConf="meterConf" />
    <PropsVue
      msg="Simple Visual <meter/> html Configuration"
      :meterConf="meterConf"
    />
  </div>
</template>

<script>
import MeterComponet from "./components/MeterComponet.vue";
import PropsVue from "./components/PropsVue";

export default {
  name: "App",

  components: { PropsVue, MeterComponet },

  data() {
    return {
      meterConf: {
        min: 0,
        max: 10,
        low: 3,
        high: 5,
        optimum: 6,
        value: 3,

        peak: 8
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


