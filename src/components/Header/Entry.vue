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
  padding: 0.5rem;
  opacity: 0;
  transform: translateY(50%);
  animation: animatein 0.3s forwards;
  border-bottom: rgba(0, 0, 0, 0.068) 1px solid;
  border-left: rgba(0, 0, 0, 0.068) 2px solid;
  width: 20rem;
}

li:hover {
  cursor: pointer;
  border-left: rgb(16, 0, 161) 2px solid;
}

@keyframes animatein {
  100% {
    opacity: 100%;
    transform: translateY(0%);
  }
}

input {
  width: 2rem;
}

select {
  width: 3.5rem;
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
