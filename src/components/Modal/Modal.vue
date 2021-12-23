<template>
  <div>
    <header>
      <searchbar @suggest="updateSuggestions" :reset="reset"/>
      <button @click="close()"><i class="fas fa-times"></i></button>
    </header>
    <ul>
      <li
        v-for="item in suggestions"
        :key="item.name"
        :item="item"
        @click="showFooter(item)"
        tabindex="0"
      >
        {{ item.name }}
      </li>
    </ul>
    <additem
      v-show="show"
      :itemSelect="itemSelect"
      @add-to-diary="addToDiary"
    />
  </div>
</template>

<script>
import searchbar from "./SearchBar.vue";
import additem from "./AddItem.vue";
export default {
  name: "modal",

  emits: ["add-to-diary"],

  components: {
    searchbar,
    additem,
  },

  data() {
    return {
      reset: false,
      show: false,
      itemSelect: "",
      suggestions: [
        {
          name: "apple",
          image: "apple.jpg",
          id: 9003,
          aisle: "Produce",
          possibleUnits: [
            "small",
            "large",
            "piece",
            "slice",
            "g",
            "extra small",
            "medium",
            "oz",
            "cup slice",
            "cup",
            "serving",
          ],
        },
      ],
    };
  },

  methods: {
    addToDiary(res) {
      this.$emit("add-to-diary", res);
      this.show = false;
    },
    updateSuggestions(res) {
      this.suggestions = res;
    },
    close() {
      this.$emit("close-modal");
      this.show = false;
      this.reset = true
    },
    showFooter(item) {
      this.itemSelect = item;
      this.show = true;
    },
  },
};
</script>

<style scoped>
header {
  display: flex;
  flex-direction: row;
  padding-top: 0.5rem;
  
  justify-content: space-around;
  flex-wrap: wrap-reverse;
  align-self: center;
  background: rgba(255, 255, 255, 0.548);
  width: 50vw;
  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
    box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.178);

}

ul {
  overflow-y: scroll;
  height: 40vh;
  margin-top: 0.5rem;
}

button {
  background: none;
  border: none;
  font-size: 1.5rem;
  color: rgb(172, 0, 0);
  justify-self: end;
  margin: 0 2rem;
}
i:hover {
  cursor: pointer;
  color: rgb(255, 96, 96);
}

div {
  display: flex;
  flex-direction: column;
  align-content: center;
  position: fixed;
  width: 50vw;
  height: fit-content;
  background: rgb(255, 255, 255);
  z-index: 1;
  border: solid 2px rgba(0, 0, 0, 0.212);
  border-radius: 10px;
  top: 5%;
  left: 50%;
  opacity: 0;
  transform: translate(-50%, -50%);
  animation: animatetop 0.4s forwards;
  box-shadow: 0px 0px 10px 5px rgba(0, 0, 0, 0.24);
}
@media screen and (max-width: 800px) {
  div,
  header {
    width: 75vw;
  }
}

@keyframes animatetop {
  100% {
    opacity: 100%;
    top: 40%;
  }
}

li {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  list-style: none;
  background: rgb(233, 233, 233);
  padding: 0.3rem;
  margin: 5px 0;
}
li:focus {
  outline: solid 2px rgb(168, 168, 168);
  background: rgb(212, 212, 212);
}
li:hover {
  cursor: pointer;
}
</style>
