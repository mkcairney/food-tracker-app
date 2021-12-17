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
  gap: 0rem;
  width: 50vw;
  height: fit-content;
  padding-bottom: 1rem;
  background: rgba(255, 255, 255, 0);
   border-radius: 10px;
}

</style>

Entry
