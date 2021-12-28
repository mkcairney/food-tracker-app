<template>
    <main>
        <container  :nutrition="nutrition.general" name="General"/>
        <container  :nutrition="nutrition.vitamins" name="Vitamins"/>
        <container  :nutrition="nutrition.minerals" name="Minerals"/>
        <!-- <container  :nutrition="nutrition.other" name="Other"/> -->
    </main>
</template>

<script>
import Container from './Container.vue'
export default {
    name: "main",
    components: {Container},
    props: ["nutrition"]
}
</script>

<style  scoped>
main {
    background: none;
    padding-top: 3rem;
  display: flex;
  flex-direction: column;
  align-content: center;
}
</style>