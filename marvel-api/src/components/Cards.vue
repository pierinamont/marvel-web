<template>
<!-- input -->
  <section class="flex justify-center items-center my-10">
    <div class="relative">
      <div class="absolute top-4 left-3">
        <i class="fa fa-search text-gray-400 z-20 hover:text-gray-500"></i>
      </div>
      <input
        v-model="search"
        v-on:keyup.enter="searchName"
        type="text"
        class="
          h-14
          w-64
          md:w-96
          pl-6
          md:pl-10
          pr-20
          rounded-lg
          z-0
          focus:shadow focus:outline-none
        "
        placeholder="search anything..."
      />
      <div class="absolute top-2 right-2">
        <button
          :click="searchName"
          class="h-10 w-20 text-white rounded-lg bg-red-600 hover:bg-red-800 text-sm"
        >
          SEARCH
        </button>
      </div>
    </div>
  </section>


<!-- Sección de cards -->
<section class="w-10/12 flex flex-wrap justify-center m-auto gap-10 mb-20">
  <div
    v-for="character in characters"
    :key="character.id"
    class="
      bg-white
      shadow-md
      border border-gray-200
      rounded-lg
      dark:bg-gray-800 dark:border-gray-700
      w-56
      md:w-64
    "
  >
    <img
      class="rounded-t-lg"
      :src="character.thumbnail.path + '.' +character.thumbnail.extension"
      alt=""
    />

    <div class="p-5">
      <h5
        class="
          text-gray-900
          font-bold
          text-xl
          tracking-tight
          mb-2
          dark:text-white
        "
      >
        {{character.name}}
      </h5>

      <p class="text-sm text-gray-700 mb-3">
         {{character.description}}
      </p>
    </div>
  </div>
</section>
</template>

<script>
// https://gateway.marvel.com:443/v1/public/characters/1017100?apikey=
import axios from "axios";

export default {
  data() {
    return {
      characters: [],
      search: "",
    };
  },
  // props: {
  //   search: ""
  // },
  methods: {
    getData() {
      console.log(this.search)
      axios
        .get(
          "http://gateway.marvel.com/v1/public/characters?ts=1&apikey=5ca0254ca03b0cb4515e99240e79f903&hash=28db8be61d0ada711c2c558e79fe9d6e"
        )
        .then((res) => {
        this.characters = res.data.data.results;
        console.log(res.data.data.results);
        })
        .catch((error) => console.log(error));
    },
    searchName() {
       axios
        .get(
          "http://gateway.marvel.com/v1/public/characters?ts=1&apikey=5ca0254ca03b0cb4515e99240e79f903&hash=28db8be61d0ada711c2c558e79fe9d6e"
        )
        .then((res) => {
        // Filtrar por nombre
        // let names = res.data.data.results.name;
        // names.filter((n) => n == this.search)
          let allData = res.data.data.results;

          if(this.search === '') {
            this.characters = allData;
          } else {
            const names = allData.filter((data) => data.name.toLowerCase().includes(this.search))
            this.characters = names;
          }
        })
        .catch((error) => console.log(error));
    },
  },
  beforeMount(){
    this.getData();
  },
  

};
</script>
