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
    @entry-focus="entryFocus"
    @entry-blur="entryBlur"
  />
  <Main :nutrition="nutrition" :macro="macro" />
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
    // method for opening and closing the food search modal
    toggleModal() {
      if (this.modal == true) {
        this.modal = false;
      } else {
        this.modal = true;
      }
    },

    // method for clearing all food entries at once
    clearAll() {
      this.diary = [];
      this.updateNutrition(this.diary);
    },

    // method for updating a food entry measurement, where payload has been bubbled up from a nested compenent using emits.
    entryChange(payload) {
      this.diary[this.diary.findIndex((entry) => entry.myid == payload.myid)] =
        payload;
      this.updateNutrition(this.diary);
    },

    // method for setting a food entry and adding a unqiue id in order to edit or delete successfully
    addToDiary(res) {
      this.diary.push({
        ...res,
        myid: Math.round(Math.random() * 10000),
        selected: true,
      });
      this.toggleModal();
      this.updateNutrition(this.diary);
    },

    //  method for removing a food entry
    deleteEntry(item) {
      this.diary = this.diary.filter((entry) => entry.myid !== item.myid);
      this.updateNutrition(this.diary);
    },

    // method for selecting a single entry from the diary on focus,
    // removing the rest of the diary from the nutrition state.
    entryFocus(item) {
      this.temp = [];
      this.temp.push(item);
      this.diary.forEach((a) => {
        if (a.myid !== item.myid) {
          a.selected = false;
        }
      });
      this.updateNutrition(this.temp);
    },

    // reseting the entries not selected to default so entire diary is included in the nutrition state.
    entryBlur() {
      this.temp = [];
      this.diary.forEach((a) => (a.selected = true));
      this.updateNutrition(this.diary);
    },

    // method for calculating the total nutrients from all diary entries
    updateNutrition(list) {
      let respNutr = list.map((entry) => entry.nutrition.nutrients).flat();
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
      temp: [],
      modal: false,
      API_KEY,
    };
  },
  computed: {
    totalMacro() {
      return (
        this.nutrition.other[0].amount +
        this.nutrition.other[1].amount +
        this.nutrition.other[2].amount
      );
    },
    macro() {
      if (this.totalMacro === 0) {
        return {
          display: "none",
        };
      } else {
        return {
          fat: `${
            Math.round(
              (this.nutrition.other[0].amount / this.totalMacro) * 1000
            ) / 10
          }%`,
          carbs: `${
            Math.round(
              (this.nutrition.other[1].amount / this.totalMacro) * 1000
            ) / 10
          }%`,
          protein: `${
            Math.round(
              (this.nutrition.other[2].amount / this.totalMacro) * 1000
            ) / 10
          }%`,
        };
      }
    },
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
