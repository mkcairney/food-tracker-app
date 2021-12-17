<template>
  <section>
      <p>General</p>
    <div>
      <nutrient :radius="60" :progress="100" :stroke="10" />
      <nutrient :radius="60" :progress="38.22" :stroke="10" />
    </div>
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
  flex-direction: column;
  gap: 1rem;
  align-content: center;
  border: solid 2px rgb(63, 63, 63);
  color: rgb(63, 63, 63);
  border-radius: 10px;
  width: 75vw;
  height: 30vh;
  padding: 0rem 2rem;
  align-self: center;
  text-align: center;
}

div {
    display: flex;
    flex-direction: row;
    gap: 2rem;
}

p {
  width: fit-content;
  font-size: 1.3rem;
  background: white;
  padding: 0 0rem;
}
</style>
