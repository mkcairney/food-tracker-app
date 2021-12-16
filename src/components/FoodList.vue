<template>
  <ul class="list-container">
    <entry
      v-for="item in diary"
      :key="item.name"
      :item="item"
      @delete-entry="$emit('delete-entry', item)"
    />
  </ul>
</template>

<script>
import Entry from "./Entry.vue";
export default {
  name: "FoodList",
  props: ["diary"],
  emits: ["delete-entry"],
  components: { Entry },
};
</script>

<style scoped>
ul {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  width: 50vw;
  min-height: 30vh;
  height: fit-content;
}

</style>

Entry
