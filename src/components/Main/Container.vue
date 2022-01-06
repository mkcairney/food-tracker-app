<template>
  <section>
    <p>{{ name }}</p>
    <div>
      <nutrient
        v-for="nutrient in nutrition"
        :key="nutrient.name"
        :progress="nutrient.percentOfDailyNeeds"
        :amount="nutrient.amount"
        :name="nutrient.name"
        :unit="nutrient.unit"
        :threshold="nutrient.threshold"
      />
    </div>
  </section>
</template>

<script>
import Nutrient from "./Nutrient.vue";
export default {
  name: "container",
  components: { Nutrient },
  props: ["nutrition", "name"],
};
</script>

<style scoped>
section {
  display: flex;
  flex-direction: column;
  gap: 0rem;
  align-content: center;
  border: solid 2px rgb(63, 63, 63);
  color: rgb(63, 63, 63);
  border-radius: 10px;
  width: 75vw;
  height: fit-content;
  overflow: visible;
  padding: 0rem 2rem;
  padding-bottom: 2rem;
  align-self: center;
  text-align: center;
  margin-bottom: 3rem;
}

div {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 2rem;
  justify-content: center;
}
@media screen and (max-width: 480px) {
  div {
    gap: 0rem;
  }
}

p {
  width: fit-content;
  font-size: 1.5rem;
  background: rgb(255, 255, 255);
  transform: translateY(-53%);
  padding: 0 0.5rem;
}
</style>
