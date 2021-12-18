<template>
  <Modal
    v-show="this.modal"
    @close-modal="toggleModal()"
    @add-to-diary="addToDiary"
  />
  <Header
    :diary="diary"
    @search-modal="toggleModal()"
    @delete-entry="deleteEntry"
  />
  <Main :nutrition="nutrition" />
</template>

<script>
import Header from "./components/Header/Header.vue";
import Modal from "./components/Modal/Modal.vue";
import Main from "./components/Main/Main.vue";

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

    async addToDiary(item) {
      // this.diary.push(item);
      // this.diary[0].nutrition.nutrients.forEach(nutrient => {
      //     this.nutrition.push(nutrient)
      // });
      // console.log(this.nutrition);
      // this.toggleModal();
      await (
        await fetch(
          `https://api.spoonacular.com/food/ingredients/${item.id}/information?amount=1&apiKey=${this.API_KEY}`
        )
      )
        .json()
        .then((response) => {
          this.diary.push(response);

          if (this.nutrition.length === 0) {
            this.nutrition = response.nutrition.nutrients;
          } else {
            response.nutrition.nutrients.forEach((nutrient) => {
              this.nutrition[
                this.nutrition.findIndex((nutr) => nutr.name == nutrient.name)
              ].amount += nutrient.amount;
            });
          }
          console.log(this.nutrition);
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
      nutrition: [
        {
          name: "Calories",
          amount: 0,
          unit: "cal",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Fat",
          amount: 0,
          unit: "g",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Saturated Fat",
          amount: 0,
          unit: "g",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Carbohydrates",
          amount: 0,
          unit: "g",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Net Carbohydrates",
          amount: 0,
          unit: "g",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Sugar",
          amount: 0,
          unit: "g",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Cholesterol",
          amount:0,
          unit: "mg",
          percentOfDailyNeeds: 0.0,
        },
        {
          name: "Sodium",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Protein",
          amount: 0,
          unit: "g",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Vitamin C",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Manganese",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Fiber",
          amount: 0,
          unit: "g",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Vitamin B6",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Copper",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Vitamin B1",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Folate",
          amount: 0,
          unit: "µg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Potassium",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Magnesium",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Vitamin B3",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Vitamin B5",
          amount:0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Vitamin B2",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Iron",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Calcium",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Vitamin A",
          amount: 0,
          unit: "IU",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Zinc",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Phosphorus",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Vitamin K",
          amount: 0,
          unit: "Âµg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Selenium",
          amount: 0,
          unit: "Âµg",
          percentOfDailyNeeds: 0,
        },
        {
          name: "Vitamin E",
          amount: 0,
          unit: "mg",
          percentOfDailyNeeds: 0,
        },
      ],

      diary: [],
      modal: false,
      API_KEY,
    };
  },
};
</script>

<style>
@import "./assets/css/styles.css";
@import url("https://fonts.googleapis.com/css2?family=Righteous&family=Ubuntu:wght@300&display=swap");
* {
  margin: 0;
  padding: 0;
  font-family: "Ubuntu", "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}

body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-repeat: no-repeat;
}
</style>
