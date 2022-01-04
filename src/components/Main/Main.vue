<template>
  <main>
    <div>
      <a :style="{ width: this.macro.protein, background: '#45a319' }"></a>
      <a :style="{ width: this.macro.carbs, background: '#145bb8' }"></a>
      <a :style="{ width: this.macro.fat, background: '#c12525' }"></a>
    </div>
    <caption>
      
    </caption>
    <container :nutrition="nutrition.general" name="General" />
    <container :nutrition="nutrition.vitamins" name="Vitamins" />
    <container :nutrition="nutrition.minerals" name="Minerals" />
    <!-- <container  :nutrition="nutrition.other" name="Other"/> -->
  </main>
</template>

<script>
import Container from "./Container.vue";
export default {
  name: "main",
  components: { Container },
  props: ["nutrition", "macro"],
  data() {
    return {
      test: { green: "20%", red: "50%", blue: "30%" },
    };
  },
};
</script>

<style scoped>
main {
  background: none;
  padding-top: 3rem;
  display: flex;
  flex-direction: column;
  align-content: center;
}
div {
  background: rgba(95, 95, 95, 0);
  margin-bottom: 2rem;
  width: 75vw;
  align-self: center;
  height: 1rem;
  display: flex;
}

a:nth-child(1) {
  transition: 0.5s;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}
a:nth-child(2) {
  transition: 0.5s;
}

a:nth-child(3) {
  transition: 0.5s;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
}

</style>
