<template>
  <section>
    <header>
      <img
        src="https://spoonacular.com/images/spoonacular-logo-b.svg"
        class="logo"
        alt="Spoonacular Logo"
        onclick="window.open('https://spoonacular.com/food-api')"
      />
      <h1>NUTRITION TRACKER</h1>
      <i class="fas fa-info-circle" tabindex="0"></i>
      <p>
        The recommended nutrient levels given are based on the RDA
        (Recommended Dietary Allowance), Adequate Intake (AI) and Tolerable
        Upper Intake Level (UL) for the average healthy adult (excluding
        pregnant women). Full information can be found
        <a
          href="https://ods.od.nih.gov/HealthInformation/Dietary_Reference_Intakes.aspx"
          target="_blank"
        >
          here</a
        >.
      </p>
    </header>

    <div>
      <my-button
        @button-click="$emit('search-modal')"
        :prop="{ name: 'ADD FOOD', icon: 'fas fa-utensils', color: 'red' }"
      />
      <my-button
        @button-click="$emit('clear-all')"
        :prop="{ name: 'CLEAR ALL', icon: 'fas fa-times-circle', color: 'red' }"
      />
    </div>

    <food-list
      :diary="diary"
      @delete-entry="deleteEntry"
      @entry-change="entryChange"
    />
  </section>
</template>

<script>
import FoodList from "./FoodList.vue";
import MyButton from "./Button.vue";

export default {
  components: { FoodList, MyButton },
  props: ["diary"],
  emits: ["search-modal", "delete-entry", "clear-all"],
  name: "Header",
  data() {
    return {
      API_KEY: process.env.API_KEY,
    };
  },
  methods: {
    entryChange(payload) {
      this.$emit("entry-change", payload);
    },

    deleteEntry(item) {
      this.$emit("delete-entry", item);
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Righteous&family=Ubuntu:wght@300&display=swap");

section {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  align-items: center;
  background: linear-gradient(rgb(68, 230, 47), rgb(0, 197, 82));
  width: 98.8vw;
  min-height: 50vh;
  height: fit-content;
  padding: 1rem 0rem;
  border-radius: 0 0 80% 80% / 20%;
}
@media screen and (max-width: 480px) {
  section {
    border-radius: 0 0 80% 80% / 15%;
  }
}

img {
  width: 3.5rem;
  justify-self: baseline;
  cursor: pointer;
}

h1 {
  font-family: "Righteous";
  text-align: center;
  color: rgba(58, 58, 58, 0.712);
  letter-spacing: 2px;
  align-self: center;
  font-size: 2rem;
}

i {
  color: rgb(255, 255, 255);
  align-self: center;
  font-size: 1.3rem;
}
i:hover {
  cursor: pointer;
  opacity: 0.7;
}

i:focus + p {
  opacity: 1;
  z-index: 50;
}

p {
  z-index: -1;
  background: white;
  border-radius: 10px;
  position: fixed;
  top: 30%;
  padding: 3rem;
  opacity: 0;
  transition: 0.7s;
  box-shadow: 0px 0px 20px 100vh rgba(0, 0, 0, 0.274);
  text-align: center;
  width: 50vw;
}

div {
  display: flex;
  flex-direction: row;
  justify-content: center;
  flex-wrap: wrap;
}

header {
  display: flex;
  flex-direction: row;
  align-content: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 0.75rem;
  width: 90vw;
}

</style>
