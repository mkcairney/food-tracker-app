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
  flex-wrap: wrap;
  justify-content: left;
  gap: 5px;
  width: 76vw;
  height: fit-content;
  padding-bottom: 2rem;
  background: rgba(255, 255, 255, 0);
   border-radius: 10px;
}

</style>

Entry
