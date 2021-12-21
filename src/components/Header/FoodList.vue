<template>
  <ul class="list-container">
    <entry
      v-for="item in diary"
      :key="item.id"
      :item="item"
      @delete-entry="$emit('delete-entry', item)"
      @entry-change="entryChange"
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
  methods: {
    entryChange(payload) {
      this.$emit("entry-change", payload);
    },
  },
};
</script>

<style scoped>
ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 5px;
  width: 90vw;
  height: fit-content;
  padding-bottom: 3rem;
  background: rgba(255, 255, 255, 0);
  border-radius: 10px;
}


</style>

Entry
