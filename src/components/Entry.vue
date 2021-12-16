<template>
  <li>
    {{ item.name }}
    <div>
      <input type="number" min="0" value="1" />
      <select name="measure" id="measure">
        <option :key="unit" value="unit" v-for="unit in item.possibleUnits">
          {{ unit }}
        </option></select
      ><button @click="this.$emit('delete-entry', item)"><i class="fas fa-trash-alt"></i></button>
    </div>
  </li>
</template>

<script>
export default {
  name: "entry",
  props: ["item"],
};
</script>

<style scoped>
li {
  list-style: none;
  background: rgb(233, 233, 233);
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  border-left: blue solid 2px;
  padding: 0.5rem;
  opacity: 0;
  transform: translateY(50%);
  animation: animatein 0.45s forwards;
  box-shadow: 3px 3px 7px rgba(0, 0, 0, 0.486);
}

@keyframes animatein {
  100% {
    opacity: 100%;
    transform: translateY(0%);
  }
}

input {
  width: 2.5rem;
}

select {
  width: 4rem;
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
    color: rgb(199, 81, 81)
}
</style>
