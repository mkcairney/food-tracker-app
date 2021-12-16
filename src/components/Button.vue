<template>
  <button @click="onAdd()">{{ prop.name }} <i :class="prop.icon"></i></button>
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
  background: linear-gradient(rgb(240, 71, 71), rgb(209, 56, 56));
  padding: 1rem;
  border: none;
  border-radius: 999px;
  color: rgb(247, 247, 247);
  margin: 1rem;
  font-size: 1.2rem;
  transition: 0.3s;
}

button:hover {
  cursor: pointer;
  filter: brightness(120%);
}
</style>
