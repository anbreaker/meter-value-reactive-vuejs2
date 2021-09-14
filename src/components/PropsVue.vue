<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <hr />

    <meter
      class="meter-container"
      :min="values.min"
      :max="values.max"
      :low="values.low"
      :high="values.high"
      :optimum="values.optimum"
      :value="values.value"
    ></meter>

    <ul>
      <li v-for="(value, index) in values" :key="index">
        {{ index }} {{ value }}
        <button @click="changeValue(index, 'sum')">+</button>
        <button @click="changeValue(index, 'rest')">-</button>
      </li>
    </ul>

    <h2>Object Props</h2>

    <button @click="showProps">Show Props</button>
  </div>
</template>

<script>
export default {
  name: "PropsVue",

  props: {
    msg: {
      type: String,
      required: true
    },

    values: {
      min: { type: Number, required: true },
      max: { type: Number, required: true },
      low: { type: Number, required: true },
      high: { type: Number, required: true },
      optimum: { type: Number, required: true },
      value: { type: Number, required: true }
    }
  },

  methods: {
    showProps() {
      console.log(this.msg, "<--- Props");
    },

    changeValue(index, type) {
      if (type === "sum") this.values[index]++;
      else this.values[index]--;
    }
  }
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
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.meter-container {
  height: 1.875rem;
  width: 50%;
}

/*
  below low: default Color RED
  equal to low to high: default Color Orange
  equal to high to max: default Color Green

  meter for Chrome
*/
meter::-webkit-meter-bar {
  background: #c6c5c5; /*background color of bar*/
}

meter::-webkit-meter-optimum-value {
  background: greenyellow; /* "green" */
}

meter::-webkit-meter-suboptimum-value {
  background: darkorange; /* "orange" */
}

meter::-webkit-meter-even-less-good-value {
  background: crimson; /* "red" */
}
</style>
