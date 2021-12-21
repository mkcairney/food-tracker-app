<template>
  <header>
    <h1>NUTRITION TRACKER</h1>

    <div>
      <diary-button
        @button-click="$emit('search-modal')"
        :prop="{ name: 'ADD FOOD', icon: 'fas fa-utensils', color: 'red' }"
      />
      <diary-button
        @button-click="$emit('clear-all')"
        :prop="{ name: 'CLEAR ALL', icon: 'fas fa-times-circle', color: 'red' }"
      />
    </div>

    <food-list
      :diary="diary"
      @delete-entry="deleteEntry"
      @entry-change="entryChange"
    />
  </header>
</template>

<script>
import FoodList from "./FoodList.vue";
import DiaryButton from "./Button.vue";

export default {
  components: { FoodList, DiaryButton },
  props: ["diary"],
  emits: ["search-modal", "delete-entry", "clear-all"],
  name: "Header",
  data() {
    return {
      trivia: "",
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
  created() {
    // this.getTrivia();
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
  background: linear-gradient(rgb(68, 230, 47), rgb(0, 197, 82));
  width: 98.8vw;
  min-height: 60vh;
  height: fit-content;
  padding: 1rem 0rem;
  border-radius: 0 0 80% 80% / 30%;
}
@media screen and (max-width: 480px) {
  header {
    border-radius: 0 0 80% 80% / 20%;
  }
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

div {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
</style>
