<template>
  <li>
    {{ item.name }}
    <div>
      <input v-model="quantity"  type="number" min="0" />
      <select name="measure" v-model="units" id="measure">
        <option :key="unit" :value="unit" v-for="unit in item.possibleUnits">
          {{ unit }}
        </option></select
      ><button @click="this.$emit('delete-entry', item)">
        <i class="fas fa-trash-alt"></i>
      </button>
    </div>
  </li>
</template>

<script>
export default {
  name: "entry",
  props: ["item"],
  data() {
    return {
      quantity: this.item.amount,
      units: this.item.unit,
      API_KEY: process.env.VUE_APP_API_KEY,
    };
  },
  watch: {
   quantity: async function changeQuantity() {
      await (
        await fetch(
          `https://api.spoonacular.com/food/ingredients/${this.item.id}/information?amount=${this.quantity}&unit=${this.units}&apiKey=${this.API_KEY}`
        )
      )
        .json()
        .then((response) => {
          this.$emit("entry-change", {...response, myid: this.item.myid})
        });
    },

    units: async function changeQuantity() {
      await (
        await fetch(
          `https://api.spoonacular.com/food/ingredients/${this.item.id}/information?amount=${this.quantity}&unit=${this.units}&apiKey=${this.API_KEY}`
        )
      )
        .json()
        .then((response) => {
          this.$emit("entry-change", {...response, myid: this.item.myid})
        });
    },
  },
};
</script>

<style scoped>
li {
  list-style: none;
  background: rgb(255, 255, 255);
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 0.5rem;
  opacity: 0%;
  animation: animatein 0.3s forwards;
  border-left: rgba(0, 255, 21, 0) 4px solid;
  border-radius: 4px;
  width: fit-content;
  transition: 0.2s;
}

li:hover {
  cursor: pointer;
  box-shadow: 3px 3px 7px rgba(0, 0, 0, 0.342);
  transform: translateY(-5%);
}

@keyframes animatein {
  100% {
    opacity: 100%;
    /* transform: translateX(0%); */
  }
}

input {
  width: 2.4rem;
  border: solid 1px rgba(128, 128, 128, 0.466);
  padding: 1px 0;
  margin-left: 1rem;
}

select {
  width: 3.5rem;
  border: solid 1px rgba(128, 128, 128, 0.445);
}

button {
  background: none;
  border: none;
  color: rgb(187, 6, 6);
  font-size: 1rem;
  margin: 0 1rem;
}
i:hover {
  cursor: pointer;
  color: rgb(199, 81, 81);
}
</style>
