<template>
  <ul class="list-container">
    <entry
      v-for="item in diary"
      :key="item.id"
      :item="item"
      @delete-entry="$emit('delete-entry', item)"
      @entry-change="entryChange"
      @entry-focus="entryFocus"
      @entry-blur="entryBlur"
    />
  </ul>
</template>

<script>
import Entry from "./Entry.vue";
export default {
  name: "FoodList",
  props: ["diary"],
  emits: ["delete-entry", "entry-focus", "entry-blur"],
  components: { Entry },
 
  methods: {
    entryChange(payload) {
      this.$emit("entry-change", payload);
    },
     entryFocus(item) {
      this.$emit("entry-focus", item);
      this.selected = item.myid
      console.log(this.selected)
    },
    entryBlur(item) {
      this.$emit("entry-blur", item);
    }
  },
};
</script>

<style  scoped>
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
