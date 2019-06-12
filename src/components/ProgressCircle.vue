<template id="progress-ring">
  <svg class="progress-ring" viewBox="-50,-50,100,100">
    <circle class="progress-ring-circle" r="46"></circle>
    <path class="progress-ring-ring" :d="path"></path>
    <circle class="progress-ring-end" :cx="endX" :cy="endY" r="4"></circle>
    <text style="font-size: 50px" alignment-baseline="middle" text-anchor="middle">{{ text }}</text>
  </svg>
</template>

<script>
export default {
  name: "progress-ring",
  props: ["max", "min", "value", "text"],
  data() {
    return {};
  },

  computed: {
    theta() {
      const frac = (this.value - this.min) / (this.max - this.min) || 0;
      return frac * 2 * Math.PI;
    },
    path() {
      const large = this.theta > Math.PI;
      return `M0,-46 A46,46,0,${large ? 1 : 0},1,${this.endX},${this.endY}`;
    },
    endX() {
      return Math.cos(this.theta - Math.PI * 0.5) * 46;
    },
    endY() {
      return Math.sin(this.theta - Math.PI * 0.5) * 46;
    }
  }
};
</script>

<style scoped>
.progress-ring {
  width: 100px;
  height: 100px;
  padding: 26px;
}

.progress-ring-circle {
  stroke: rgba(0, 0, 0, 0.1);
  stroke-width: 1;
  fill: none;
}

.progress-ring-ring {
  stroke: #007fff;
  stroke-width: 2;
  fill: none;
}

.progress-ring-end {
  fill: #007fff;
}
</style>
