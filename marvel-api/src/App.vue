<template>
  <Header />
    <Cards />
  <Footer />
</template>

<script>
import Cards from './components/Cards.vue';
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    Cards,
    Footer,
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  /* -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px; */
  background-color: rgb(244, 246, 253);
}
</style>