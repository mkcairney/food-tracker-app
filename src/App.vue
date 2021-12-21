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
    @entry-change="entryChange"
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
    entryChange(payload) {
      this.diary[this.diary.findIndex((entry) => entry.myid == payload.myid)] =
        payload;
      this.updateNutrition();
    },

    addToDiary(item) {
      this.diary.push({ ...item, myid: Math.round(Math.random() * 10000) });
      this.toggleModal();
    },

    deleteEntry(item) {
      this.diary = this.diary.filter((entry) => entry.myid !== item.myid);
      this.updateNutrition();
    },

    updateNutrition() {
      let respNutr = this.diary
        .map((entry) => entry.nutrition.nutrients)
        .flat();
      this.nutrition.general
        .concat(this.nutrition.vitamins)
        .concat(this.nutrition.minerals)
        .concat(this.nutrition.other)
        .forEach((nutr) => {
          nutr.amount = 0;
          nutr.percentOfDailyNeeds = 0;
          respNutr.forEach((nutrient) => {
            if (nutr.name == nutrient.name) {
              nutr.amount += nutrient.amount;
              nutr.percentOfDailyNeeds += Math.round(
                (nutr.amount / nutr.dailyNeeds) * 100
              );
            }
          });
        });
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
