<template>
  <main>
    <p>
      {{ Math.round(this.nutrition.general[0].amount) }}

      <br />
      <span>kcal</span>
      
    </p>
    <!-- <nutrient 
        :style="{alignSelf: 'center', marginBottom: '1rem'}"
        :progress="this.nutrition.general[0].percentOfDailyNeeds"
        :amount="Math.round(this.nutrition.general[0].amount)"
        name="Calories"
        unit=""
        :threshold="this.nutrition.general[0].threshold"/> -->
    <div>
      <section
        :style="{
          width: this.macro.protein,
          background: '#45a319',
          display: this.macro.display,
        }"
      ></section>
      <section
        :style="{
          width: this.macro.carbs,
          background: '#145bb8',
          display: this.macro.display,
        }"
      ></section>
      <section
        :style="{
          width: this.macro.fat,
          background: '#c12525',
          display: this.macro.display,
        }"
      ></section>
    </div>
    <ul>
      <li><strong> Protein </strong> {{ macro.protein }}</li>
      <li><strong> Net Carbs </strong> {{ macro.carbs }}</li>
      <li><strong> Fat </strong>{{ macro.fat }}</li>
    </ul>
    <!-- <container :nutrition="nutrition.general" name="General" /> -->
    <container :nutrition="nutrition.vitamins" name="Vitamins" />
    <container :nutrition="nutrition.minerals" name="Minerals" />
    <!-- <container  :nutrition="nutrition.other" name="Other"/> -->
  </main>
</template>

<script>
import Container from "./Container.vue";
export default {
  name: "main",
  components: { Container },
  props: ["nutrition", "macro"],
};
</script>

<style scoped>
main {
  background: none;
  padding-top: 1rem;
  display: flex;
  flex-direction: column;
  align-content: center;
}
p {
  align-self: center;
  font-size: 1.5rem;
  margin-bottom: 1rem;
  border: 5px solid rgba(0, 0, 0, 0.322);
  border-radius: 15px;
  padding: 0.5rem 1.5rem;
  text-align: center;
  font-weight: bold;
  color: rgba(0, 0, 0, 0.829)
}
span {
  font-size: 1.25rem;
  color: rgba(63, 63, 63, 0.795)
}
div {
  background: rgba(95, 95, 95, 0.301);
  margin-bottom: 1rem;
  width: 75vw;
  align-self: center;
  height: 1.25rem;
  display: flex;
  border-radius: 10px;
}

section:nth-child(1) {
  transition: 0.5s;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}
section:nth-child(2) {
  transition: 0.5s;
  margin: 0 3px;
}

section:nth-child(3) {
  transition: 0.5s;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
}

ul {
  list-style: none;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-content: center;
  gap: 4rem;
  margin-bottom: 2rem;
  width: 75vw;
  align-self: center;
}

li {
  position: relative;
  color: rgba(0, 0, 0, 0.795);
}

li::before {
  content: "\2022";
  position: absolute;
  left: -0.55em;
  top: -0.85rem;
  font-size: 2.5rem;
}

li:nth-child(1)::before {
  color: #45a319;
}
li:nth-child(2)::before {
  color: #145bb8;
}
li:nth-child(3)::before {
  color: #c12525;
}

strong {
  color: rgba(0, 0, 0, 0.829);
}
</style>
