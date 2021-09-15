<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <hr />

    <meter
      class="meter-container"
      :min="meterConf.min"
      :max="meterConf.max"
      :low="meterConf.low"
      :high="meterConf.high"
      :optimum="meterConf.optimum"
      :value="meterConf.value"
    ></meter>

    <ul>
      <li v-for="(value, index) in meterConf" :key="index">
        {{ index }} {{ value }}
        <button @click="changeValue(index, 'rest')">-</button>
        <button @click="changeValue(index, 'sum')">+</button>
      </li>
    </ul>

    <h2><b>meter for Chrome</b></h2>

    <p>
      Below <u><b>low</b></u
      >: default Color RED
    </p>
    <p>
      Equal to <u><b>low</b></u> to <u><b>high</b></u
      >: default Color Orange
    </p>
    <p>
      Equal to <u><b>high</b></u> to <u><b>max</b></u
      >: default Color Green
    </p>

    <p>
      You should open the Developer tools and use the extension of Chrome of
      VueJsBeta and console.
    </p>

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

    meterConf: {
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
      if (type === "sum") this.meterConf[index]++;
      else this.meterConf[index]--;
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
  font-size: 1.5rem;
  display: inline-block;
  margin: 0 10px;
}
u {
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
