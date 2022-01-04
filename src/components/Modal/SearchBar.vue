<template>
  <input
    id="searchbar"
    placeholder="Search"
    v-model="input"
    type="text"
    autocomplete="off"
  />
</template>

<script>
export default {
  name: "search-bar",
  props: ["show"],
  data() {
    return {
      input: "",
      API_KEY: process.env.VUE_APP_API_KEY,
    };
  },
  watch: {
    input: async function getFood() {
      await (
        await fetch(
          `https://api.spoonacular.com/food/ingredients/autocomplete?query=${this.input}&number=100&metaInformation=true&apiKey=${this.API_KEY}`
        )
      )
        .json()
        .then((response) => {
          this.$emit("suggest", response);
        });
    },
    
  },
  
};
</script>

<style scoped>
#searchbar {
  border: solid rgb(56, 56, 56) 2px;
  border-radius: 999px;
  background: none;
  justify-self: center;
  padding: 0.5rem 1rem;
  margin: 1rem 1rem;
  font-size: 1rem;
  flex-grow: 2;
}
</style>
