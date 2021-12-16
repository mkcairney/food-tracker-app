<template>
  <Header
    :diary="diary"
    @search-modal="toggleModal()"
    @delete-entry="deleteEntry"
  />
  <Modal
    v-show="this.modal"
    @close-modal="toggleModal()"
    @add-to-diary="addToDiary"
  />
</template>

<script>
import Header from "./components/Header.vue";
import Modal from "./components/Modal/Modal.vue";

export default {
  name: "App",
  components: {
    Header,
    Modal,
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
      this.diary.push(item);
      this.toggleModal();
      // await (
      //   await fetch(
      //     `https://api.spoonacular.com/food/ingredients/${item.id}/information?amount=1&apiKey=${this.API_KEY}`
      //   )
      // )
      //   .json()
      //   .then((response) => {
      //     this.diary.push(response);

      //     this.toggleModal();
      //   });
    },

    deleteEntry(item) {
      this.diary = this.diary.filter((entry) => entry.id !== item.id);
    },
  },
  data() {
    return {
      diary: [],
      modal: false,
      API_KEY: process.env.API_KEY
    };
  },
  created() {},
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
