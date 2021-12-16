<template>
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
</template>

<script>

import axios from "axios";

export default {
  data() {
    return {
      characters: [],
    };
  },
   beforeMount(){
    this.getData();
  },
  methods: {
    getData() {
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
  },
};
</script>
