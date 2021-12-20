<template>
  <svg
   
    :height="radius * 2"
    :width="radius * 2"
  >
    <circle
    
      stroke="#c7c7c7"
      :stroke-dasharray="circumference"
      :style="{ strokeDashoffset: 0 }"
      :stroke-width="10"
      fill="transparent"
      :r="normalizedRadius"
      :cx="radius"
      :cy="radius"
    />
    <circle
      stroke="#dd4dff"
      :stroke-dasharray="circumference"
      :style="{ strokeDashoffset: strokeDashoffset }"
      :stroke-width="10"
      fill="transparent"
      :r="normalizedRadius"
      :cx="radius"
      :cy="radius"
    />

    <text
     @mouseenter="changeStat()"
    
      v-if="percent"
      fill="black"
      font-size="20"
      font-family="Verdana"
      x="50%"
      y="45%"
      dominant-baseline="middle"
      text-anchor="middle"
    >
      {{ progress }}%
    </text>
    <text
    @mouseleave="changeStat()"
      v-else
      fill="black"
      font-size="20"
      font-family="Verdana"
      x="50%"
      y="45%"
      dominant-baseline="middle"
      text-anchor="middle"
    >
      {{ amount }}{{unit}}
    </text>
    <text
      fill="black"
      font-size="13"
      text-align="center"
      font-family="Verdana"
      x="50%"
      y="60%"
      dominant-baseline="middle"
      text-anchor="middle"
    >
      {{ name }}
    </text>
  </svg>
</template>

<script>
export default {
  name: "nutrient",
  props: {
    progress: Number,
    name: String,
    amount: Number,
    unit: String
  },
  data() {
    const radius = 70;
    const normalizedRadius = radius - 10 * 2;
    const circumference = normalizedRadius * 2 * Math.PI;
    return {
      radius,
      normalizedRadius,
      circumference,
      percent: true,
    };
  },
  methods: {
    changeStat() {
      if (this.percent === true) {
        this.percent = false;
      } else {
        this.percent = true;
      }
    },
  },

  computed: {
    strokeDashoffset() {
      return (
        this.circumference - ((this.progress + 0) / 100) * this.circumference
      );
    },
  },
};
</script>

<style scoped>
circle {
  transition: stroke-dashoffset 0.35s;
  transform: rotate(-90deg);
  transform-origin: 50% 50%;
}
svg:hover {
  cursor: default
}
</style>
