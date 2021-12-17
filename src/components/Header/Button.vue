<template>
  <button @click="onAdd()"> <i :class="prop.icon"></i> {{ prop.name }}</button>
</template>

<script>
export default {
  name: "Button",
  props: {
    prop: Object,
  },
  methods: {
    onAdd() {
      this.$emit("search-modal");
    },
  },
};
</script>

<style scoped>
button {
  background: #fcfcfc;
  padding: 1rem;
  border: none;
  border-radius: 999px;
  color: rgb(63, 63, 63);
  margin: 1rem;
  font-size: 1.2rem;
  font-weight: 900;
  transition: 0.2s;
  box-shadow: 3px 3px 7px rgba(0, 0, 0, 0.308);
  word-spacing: 3px;
  letter-spacing: 1px;
}

button:hover {
  cursor: pointer;
  background: rgba(255, 255, 255, 0.699);
}
</style>
