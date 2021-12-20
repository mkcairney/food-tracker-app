<template>
  <Modal
    v-show="this.modal"
    @close-modal="toggleModal()"
    @add-to-diary="addToDiary"
  />
  <Header
    :diary="diary"
    @search-modal="toggleModal()"
    @clear-all="clearAll()"
    @delete-entry="deleteEntry"
  />
  <Main :nutrition="nutrition" />
</template>

<script>
import Header from "./components/Header/Header.vue";
import Modal from "./components/Modal/Modal.vue";
import Main from "./components/Main/Main.vue";
import data from "./assets/data.json";

export default {
  name: "App",
  components: {
    Header,
    Modal,
    Main,
  },
  methods: {
    toggleModal() {
      if (this.modal == true) {
        this.modal = false;
      } else {
        this.modal = true;
      }
    },
    clearAll() {
      this.diary = [];
    },
    async addToDiary(item) {
      await (
        await fetch(
          `https://api.spoonacular.com/food/ingredients/${item.id}/information?amount=1&apiKey=${this.API_KEY}`
        )
      )
        .json()
        .then((response) => {
          this.diary.push(response);
          // response.nutrition.nutrients.forEach((nutrient) => {
          //   let myNutr =
          //     this.nutrition[
          //       this.nutrition.findIndex((nutr) => nutr.name == nutrient.name)
          //     ];
          //   myNutr.amount += nutrient.amount;
          //   myNutr.percentOfDailyNeeds +=
          //     Math.round((myNutr.amount / myNutr.dailyNeeds) * 1000) / 10;
          // });
          let respNutr = response.nutrition.nutrients;
          this.nutrition.general
            .concat(this.nutrition.vitamins)
            .concat(this.nutrition.minerals)
            .concat(this.nutrition.other)
            .forEach((nutr) => {
              respNutr.forEach((nutrient) => {
                if (nutr.name == nutrient.name) {
                  nutr.amount += nutrient.amount;
                  nutr.percentOfDailyNeeds +=
                    Math.round((nutr.amount / nutr.dailyNeeds) * 1000) / 10;
                }
              });
            });

          this.toggleModal();
        });
    },

    deleteEntry(item) {
      this.diary = this.diary.filter((entry) => entry.id !== item.id);
    },
  },
  data() {
    const API_KEY = process.env.VUE_APP_API_KEY;
    return {
      nutrition: data,
      diary: [],
      modal: false,
      API_KEY,
    };
  },
};
</script>

<style>
@import "./assets/css/styles.css";
@import url("https://fonts.googleapis.com/css2?family=Righteous&family=Work+Sans&display=swap");
* {
  margin: 0;
  padding: 0;
  font-family: "Work Sans", "Lucida Sans", "Lucida Sans Regular",
    "Lucida Grande", "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}

body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-repeat: no-repeat;
}
</style>
