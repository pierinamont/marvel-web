<template>
  <HelloWorld />
  <Cards />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import Cards from './components/Cards.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Cards,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  /* -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px; */
}
</style>
