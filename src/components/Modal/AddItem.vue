<template>
  <section>
    {{ itemSelect.name }}
    <div>
      <input type="number" min="0"/>
      <select name="unitselect" id="unit">
        <option
          v-for="unit in itemSelect.possibleUnits"
          :key="unit"
          value="unit"
        >
          {{ unit }}
        </option>
      </select>
    </div>
    <button>Add</button>
  </section>
</template>

<script>
export default {
  name: "AddItem",
  props: ["itemSelect"],
};
</script>

<style scoped>
section {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding: 1.5rem 0;
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
