<template>
  <svg :height="60 * 2 + 10" :width="60 * 2 + 20">
    <circle
      stroke="#c7c7c7"
      :stroke-dasharray="circumference"
      :style="{ strokeDashoffset: 0 }"
      :stroke-width="10"
      fill="transparent"
      :r="normalizedRadius"
      :cx="60"
      :cy="60"
    />
    <circle
      stroke="#dd4dff"
      :stroke-dasharray="circumference"
      :style="{ strokeDashoffset: strokeDashoffset }"
      :stroke-width="10"
      fill="transparent"
      :r="normalizedRadius"
      :cx="60"
      :cy="60"
    />

    <text
      fill="black"
      font-size="20"
      font-family="Verdana"
      x="46%"
      y="50%"
      dominant-baseline="middle"
      text-anchor="middle"
    >
      {{ progress }}%
    </text>
    <text
      fill="black"
      font-size="15"
      font-family="Verdana"
      x="46%"
      y="95%"
      dominant-baseline="middle"
      text-anchor="middle"
    >
    {{name}}
    </text>
  </svg>

</template>

<script>
export default {
  name: "nutrient",
  props: {
    progress: Number,
    name: String
  },
  data() {
    
    const normalizedRadius = 60 - 10 * 2;
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
