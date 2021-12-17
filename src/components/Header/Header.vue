<template>
  <header>
    <h1>NUTRITION TRACKER</h1>

    <div>
      <diary-button @search-modal="$emit('search-modal')" :prop="{name: 'ADD FOOD',icon: 'fas fa-utensils', color: 'red'}"/>
    </div>

    <food-list :diary="diary" @delete-entry="deleteEntry" />
    <!-- <h3 :trivia="trivia">
      Did you know: <br />
      <br />
      {{ trivia }}
    </h3> -->
  </header>
</template>

<script>
import FoodList from "./FoodList.vue";
import DiaryButton from "./Button.vue";

export default {
  components: { FoodList, DiaryButton },
  props: ["diary"],
  emits: ["search-modal", "delete-entry"],
  name: "Header",
  data() {
    return {
      trivia: "",
      API_KEY: process.env.API_KEY
    };
  },
  methods: {
    async getTrivia() {
      await (
        await fetch(
          `https://api.spoonacular.com/food/trivia/random?apiKey=${this.API_KEY}`
        )
      )
        .json()
        .then((response) => {
          this.trivia = response.text;
        });
    },

    deleteEntry(item) {
      this.$emit("delete-entry", item);
    },
  },
  created() {
    this.getTrivia();
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Righteous&family=Ubuntu:wght@300&display=swap");

header {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  align-items: center;
  background: linear-gradient(rgb(68, 230, 47),rgb(0, 197, 82)) ;
  width: 100vw;
  min-height: 50vh;
  height: fit-content;
  padding: 1rem 0rem;
 border-radius:  0 0 80% 80% / 30%;
}
h1 {
  font-family: "Righteous";
  text-align: center;
  color: rgba(58, 58, 58, 0.712);
  letter-spacing: 2px;
}
h3 {
  font-size: 0.7rem;
  font-weight: 100;
  text-align: center;
  width: 50vw;
}
</style>
