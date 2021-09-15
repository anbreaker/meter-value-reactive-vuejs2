<template>
  <div class="progressbar-container">
    <!-- TODO MEDIDOR actual: 749 mínimo: 1000 máximo: 1700 max: 2000 peak: el triángulo invertido-->
    <h1>Total System Load</h1>
    <h2>{{ meterConf.value }} Kw</h2>
    <div
      class="progressbar-container__arrow-down"
      :style="positionCssVar(meterConf.peak, divContainerSize)"
    ></div>
    <div class="progressbar-container__chart">
      <!--Below "low": default Color RED - Equal to "low" to "high": default Color Orange - Equal to "high" to max: default Color Green-->
      <meter
        class="progressbar-container__chart--meter"
        :min="meterConf.min"
        :max="meterConf.max"
        :low="meterConf.low"
        :high="meterConf.high"
        :optimum="meterConf.optimum"
        :value="meterConf.value"
      ></meter>
      <div class="progressbar-container__color">
        <div
          class="progressbar-container__color--opt"
          :class="changeClassMark"
          :style="positionCssVar(meterConf.low, divContainerSize)"
        ></div>
        <div
          class="progressbar-container__color--dng"
          :style="positionCssVar(meterConf.high, divContainerSize)"
        ></div>
      </div>
      <div class="progressbar-container__pos" ref="progressbarWidth">
        <div
          class="progressbar-container__pos--1"
          :style="positionCssVar(meterConf.min, divContainerSize)"
        >
          {{ meterConf.min }}
        </div>
        <div
          class="progressbar-container__pos--2"
          :style="positionCssVar(meterConf.low, divContainerSize)"
        >
          {{ meterConf.low }}
        </div>
        <div
          class="progressbar-container__pos--3"
          :style="positionCssVar(meterConf.value, divContainerSize)"
        >
          {{ meterConf.value }}
        </div>
        <div
          class="progressbar-container__pos--4"
          :style="positionCssVar(meterConf.high, divContainerSize)"
        >
          {{ meterConf.high }}
        </div>
        <div
          class="progressbar-container__pos--5"
          :style="positionCssVar(meterConf.peak, divContainerSize)"
        >
          {{ meterConf.peak }}
        </div>
        <div
          class="progressbar-container__pos--6"
          :style="positionCssVar(meterConf.max, divContainerSize)"
        >
          {{ meterConf.max }}
        </div>
      </div>

      <br /><br />
      <hr />
      <button @click="changevalue">Change Current Value</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProgressBar",

  props: {
    meterConf: {
      min: { type: Number, required: true },
      max: { type: Number, required: true },
      low: { type: Number, required: true },
      high: { type: Number, required: true },
      optimum: { type: Number, required: true },
      value: { type: Number, required: true },

      peak: { type: Number, required: true }
    }
  },

  data() {
    return {
      divContainerSize: 0,
      marginLeft: 0,

      color: "green",
      font: {
        weight: "800"
      }
    };
  },

  methods: {
    positionCssVar(value, width) {
      if (width) {
        let valuePercent = (value * 100) / this.meterConf.max;

        if (valuePercent === 0)
          return { "--data-position": valuePercent + "%" };
        else return { "--data-position": valuePercent + "%" };
      }
    },

    colorMark() {
      console.log("ver algo");
    },

    changevalue() {
      this.meterConf.value === 8
        ? (this.meterConf.value = 2)
        : (this.meterConf.value = 8);
    },

    handleResize() {
      if (this.$refs.progressbarWidth) {
        this.divContainerSize = this.$refs.progressbarWidth.clientWidth;
      }
    }
  },

  computed: {
    changeClassMark() {
      return this.meterConf.low <= this.meterConf.value
        ? "progressbar-container__color--opt"
        : "progressbar-container__color--opt_2";
    }
  },

  // TODO delete if not necessary
  watch: {
    divContainerSize(newValue, oldValue) {
      console.log({ oldValue, newValue });
    }
  },

  mounted() {
    this.divContainerSize = this.$refs.progressbarWidth.clientWidth;

    window.addEventListener("resize", this.handleResize);
  },

  beforeDestroy() {
    console.log("destroy");
    window.removeEventListener("resize", this.handleResize);
  }
};
</script>

<style scoped>
.progressbar-container {
  margin-left: 1rem;
  margin-right: 1rem;
  position: relative;
}

.progressbar-container h2 {
  font-size: 1.2rem;
  font-weight: bold;
  margin-bottom: 1rem;
  margin-top: 1rem;
}

.progressbar-container h1 {
  font-weight: bold;
  margin-bottom: 1rem;
  margin-top: 1rem;
}

.progressbar-container__arrow-down {
  border-left: 8px solid transparent;
  border-right: 8px solid transparent;
  border-top: 16px solid #000;
  height: 0;
  margin-left: var(--data-position);
  position: absolute;
  width: 0;
  z-index: 10;
}

.progressbar-container__color {
  display: block;
}

.progressbar-container__color--opt {
  border-left: 4px solid lightgray;
  display: block;
  height: 20px;
  margin-left: var(--data-position);
  margin-top: -24px;
  position: absolute;
  z-index: 20;
}

.progressbar-container__color--opt_2 {
  border-left: 4px solid orange;
}

.progressbar-container__color--dng {
  border-left: 4px solid crimson;
  display: block;
  height: 20px;
  margin-left: var(--data-position);
  margin-top: -24px;
  position: absolute;
  z-index: 30;
}

.progressbar-container__chart--meter {
  height: 1.875rem;
  width: 100%;
}

.progressbar-container__pos {
  position: relative;
  margin-right: 1.5rem;
}

.progressbar-container__pos--1 {
  position: absolute;
  margin-left: var(--data-position);
}

.progressbar-container__pos--2 {
  position: absolute;
  margin-left: var(--data-position);
}

.progressbar-container__pos--3 {
  position: absolute;
  margin-left: var(--data-position);
}

.progressbar-container__pos--4 {
  position: absolute;
  margin-left: var(--data-position);
}

.progressbar-container__pos--5 {
  position: absolute;
  margin-left: var(--data-position);
}

.progressbar-container__pos--6 {
  position: absolute;
  margin-left: var(--data-position);
}

/*
  Below "low": default Color RED
  Equal to "low" to "high": default Color Orange
  Equal to "high" to max: default Color Green

  meter for Chrome
*/
meter::-webkit-meter-bar {
  background: lightgray; /*background color of bar*/
}

meter::-webkit-meter-optimum-value {
  background: yellowgreen; /* "green" */
}

meter::-webkit-meter-suboptimum-value {
  background: orange; /* "orange" */
}

meter::-webkit-meter-even-less-good-value {
  background: crimson; /* "red" */
}

meter::-webkit-meter-optimum-value,
meter::-webkit-meter-suboptimum-value,
meter::-webkit-meter-even-less-good-value {
  transition: ease-in-out 1s width;
}
</style>
