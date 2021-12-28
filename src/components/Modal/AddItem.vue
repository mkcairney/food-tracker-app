<template>
  <section>
    <p>
      {{ itemSelect.name }}
    </p>
    <div>
      <input v-model="quant" type="number" min="0" />
      <select v-model="units" name="unitselect" id="unit">
        <option
          v-for="unit in itemSelect.possibleUnits"
          :key="unit"
          :value="unit"
        >
          {{ unit }}
        </option>
      </select>
    </div>
    <button @click="addToDiary(itemSelect)">Add</button>
  </section>
</template>

<script>
export default {
  name: "AddItem",
  props: ["itemSelect"],
  data() {
    return {
      quant: 1,
      units: "g",
      API_KEY: process.env.VUE_APP_API_KEY,
    };
  },
  methods: {
    async addToDiary(item) {
      await (
        await fetch(
          `https://api.spoonacular.com/food/ingredients/${item.id}/information?amount=${this.quant}&unit=${this.units}&apiKey=${this.API_KEY}`
        )
      )
        .json()
        .then((response) => {
          this.$emit("add-to-diary", response);
          this.quant = 1;
          this.units = "g";
        });
    },
  },
};
</script>

<style  scoped>
section {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  padding: 1rem 0;
  box-shadow: 0px -5px 5px rgba(0, 0, 0, 0.116);
  z-index: 555;
}
p {
  align-self: center;
  font-size: 1.2rem;
}
div {
  display: flex;
  gap: 0.5rem;
}
input {
  width: 4rem;
  border: solid 1px rgb(49, 49, 49);
  border-radius: 5px;
  padding: 1px 0;
  padding-left: 10px;
}

select {
  border: solid 1px rgb(49, 49, 49);
  border-radius: 5px;
}

button {
  border: none;
  background: rgb(5, 163, 0);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 999px;
}
button:hover {
  cursor: pointer;
  opacity: 70%;
}
</style>
