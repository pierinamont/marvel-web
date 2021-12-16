<template>
  <Header />
  <SearchInput />
  <Cards />
  <Footer />
</template>

<script>
import Cards from './components/Cards.vue';
import SearchInput from './components/SearchInput.vue'
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    Cards,
    SearchInput,
    Footer,
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
