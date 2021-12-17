<template>
  <svg :height="radius * 2" :width="radius * 2">
    <circle
      stroke="#c7c7c7"
      :stroke-dasharray="circumference"
      :style="{ strokeDashoffset: 0 }"
      :stroke-width="stroke"
      fill="transparent"
      :r="normalizedRadius"
      :cx="radius"
      :cy="radius"
    />
    <circle
      stroke="#dd4dff"
      :stroke-dasharray="circumference"
      :style="{ strokeDashoffset: strokeDashoffset }"
      :stroke-width="stroke"
      fill="transparent"
      :r="normalizedRadius"
      :cx="radius"
      :cy="radius"
    />

    <text
      fill="black"
      font-size="20"
      font-family="Verdana"
      x="51%"
      y="50%"
      dominant-baseline="middle"
      text-anchor="middle"
    >
      {{ progress }}%
    </text>
    <text
      fill="black"
      font-size="20"
      font-family="Verdana"
      x="51%"
      y="100%"
      dominant-baseline="middle"
      text-anchor="middle"
    >
      {{ progress }}%
    </text>
  </svg>
  <caption>
    Calories
  </caption>
</template>

<script>
export default {
  name: "nutrient",
  props: {
    radius: Number,
    progress: Number,
    stroke: Number,
  },
  data() {
    const normalizedRadius = this.radius - this.stroke * 2;
    const circumference = normalizedRadius * 2 * Math.PI;
    return {
      normalizedRadius,
      circumference,
    };
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
</style>
