<template>
    <main>
        <container/>
    </main>
</template>

<script>
import Container from './Container.vue'
export default {
    name: "main",
    components: {Container}
}
</script>

<style scoped>
main {
    background: none;
    padding-top: 3rem;
  display: flex;
  flex-direction: column;
  align-content: center;
}
</style>