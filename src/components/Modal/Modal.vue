<template>
  <div>
    <header>
      <searchbar @suggest="updateSuggestions" />
      <button @click="close()"><i class="fas fa-times"></i></button>
    </header>
    <ul>
      <item
         v-for="item in suggestions"
      :key="item.name"
      :item="item"
        @add-to-diary="$emit('add-to-diary', item)"
      />
    </ul>
  </div>
</template>

<script>
import searchbar from "./SearchBar.vue";
import item from "./Item.vue";
export default {
  name: "modal",

  emits: ["add-to-diary"],

  components: {
    searchbar,
    item,
  },

  data() {
    return {
      suggestions: [
    {
        "name": "apple",
        "image": "apple.jpg",
        "id": 9003,
        "aisle": "Produce",
        "possibleUnits": [
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
            "serving"
        ]
    },
    {
        "name": "applesauce",
        "image": "applesauce.png",
        "id": 9019,
        "aisle": "Canned and Jarred",
        "possibleUnits": [
            "g",
            "oz",
            "cup",
            "serving",
            "tablespoon"
        ]
    },
    {
        "name": "apple juice",
        "image": "apple-juice.jpg",
        "id": 9016,
        "aisle": "Beverages",
        "possibleUnits": [
            "g",
            "drink box",
            "fl oz",
            "oz",
            "teaspoon",
            "cup",
            "serving",
            "tablespoon"
        ]
    },
    {
        "name": "apple cider",
        "image": "apple-cider.jpg",
        "id": 1009016,
        "aisle": "Beverages",
        "possibleUnits": [
            "g",
            "drink box",
            "fl oz",
            "oz",
            "teaspoon",
            "bottle NFS",
            "cup",
            "serving",
            "tablespoon"
        ]
    },
    {
        "name": "apple jelly",
        "image": "apple-jelly.jpg",
        "id": 10019297,
        "aisle": "Nut butters, Jams, and Honey",
        "possibleUnits": [
            "g",
            "oz",
            "packet",
            "teaspoon",
            "cup",
            "serving",
            "tablespoon"
        ]
    }
],
    };
  },

  methods: {
    updateSuggestions(res) {
      this.suggestions = res;
    },
    close() {
      this.$emit("close-modal");
    },
  },
};
</script>

<style scoped>
header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-self: center;
  background: rgba(187, 187, 187, 0.548);
  width: 50vw;
  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
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
  height: 65vh;
  background: rgb(255, 255, 255);
  z-index: 1;
  border: solid 2px rgba(0, 0, 0, 0.452);
  border-radius: 10px;
  top: 5%;
  left: 50%;
  opacity: 0;
  transform: translate(-50%, -50%);
  animation: animatetop 0.4s forwards;
  box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.158);
}

@keyframes animatetop {
  100% {
    opacity: 100%;
    top: 40%;
  }
}
</style>
