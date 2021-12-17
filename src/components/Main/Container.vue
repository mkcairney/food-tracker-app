<template>
  <section>
    <nutrient />
    <nutrient />
  </section>
</template>

<script>
import Nutrient from "./Nutrient.vue";
export default {
  name: "container",
  components: { Nutrient },
};
</script>

<style scoped>
section {
  display: flex;
  flex-direction: row;
  gap: 1rem;
  align-content: center;
  border: solid 2px rgb(63, 63, 63);
  color: rgb(63, 63, 63);
  border-radius: 10px;
  width: 75vw;
  height: 30vh;
  padding: 0rem 1rem;
  align-self: center;
  text-align: center;
}

p {
  width: fit-content;
  font-size: 1.3rem;
  background: white;
  transform: translateY(-180%);
  padding: 0 0rem;
}
</style>
