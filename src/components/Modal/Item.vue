<template>
  <li @focus="showAmount" @blur="showAmount" tabindex="0">
    {{ item.name }}
    <div>
      <button @click="addToDiary(item)">
        <i class="far fa-plus-square"></i>
      </button>
    </div>
  </li>
</template>

<script>
export default {
  name: "item",
  props: ["item"],

  data() {
    return {};
  },

  methods: {
    addToDiary(item) {
      this.$emit("add-to-diary", item);
    },
  },
};
</script>

<style scoped>
li {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  list-style: none;
  background: rgb(233, 233, 233);
  padding: 1rem;
  margin: 5px 0;
  
}
li:focus {
  outline: solid 2px rgb(168, 168, 168);
  background: rgb(212, 212, 212);
}
li:hover {
  cursor: pointer;
}




div {
  display: flex;
  flex-direction: row;
}

input {
  width: 3vw;
  border: none;
}

button {
  background: none;
  border: none;
  font-size: 1.3rem;
  padding: 0rem;
  margin-left: 1rem;
}
i:hover {
  cursor: pointer;
  color: rgb(87, 194, 93);
}
</style>
