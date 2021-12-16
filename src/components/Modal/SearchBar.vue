<template>
  <input id="searchbar" placeholder="Search" v-model="input" type="text" />
</template>

<script>
export default {
  name: "search-bar",
  data() {
    return {
      input: "",
      API_KEY: process.env.API_KEY
    };
  },
  watch: {
    input: async function getFood() {
      await (
        await fetch(
          `https://api.spoonacular.com/food/ingredients/search?query=${this.input}&number=5&metaInformation=true&apiKey=${this.API_KEY}`
        )
      )
        .json()
        .then((response) =>  {
          this.$emit("suggest", response)
          });
        
    },
  },
  methods: {},
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
