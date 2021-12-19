<template>
  <section>
    <p>General</p>
    <div>
      <nutrient v-for="nutrient in nutrition.general" :key="nutrient.name" :progress="nutrient.percentOfDailyNeeds" :name="nutrient.name"/>
    </div>
    
  </section>
  <section>
    <p>Vitamins</p>
    <div>
      <nutrient v-for="nutrient in nutrition.vitamins" :key="nutrient.name" :progress="nutrient.percentOfDailyNeeds" :name="nutrient.name"/>
    </div>
    
  </section>
  <section>
    <p>Minerals</p>
    <div>
      <nutrient v-for="nutrient in nutrition.minerals" :key="nutrient.name" :progress="nutrient.percentOfDailyNeeds" :name="nutrient.name"/>
    </div>
    
  </section>
</template>

<script>
import Nutrient from "./Nutrient.vue";
export default {
  name: "container",
  components: { Nutrient },
  props: ["nutrition"],
 
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

p {
  width: fit-content;
  font-size: 1.3rem;
  background: rgb(255, 255, 255);
  transform: translateY(-53%);
  padding: 0 0.5rem;
}
</style>
