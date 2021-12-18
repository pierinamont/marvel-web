<template>
<!-- input -->
  <section class="flex justify-center items-center my-10 flex-col">
    <a 
    @click="getData"
    class="mb-5 text-red-600 cursor-pointer hover:text-blue-600">See All Characters</a>
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
          v-on:click="searchName"
          class="h-10 w-20 text-white rounded-lg bg-red-600 hover:bg-red-500 text-sm"
        >
          SEARCH
        </button>
      </div>
    </div>
  </section>


<!-- Sección de cards -->
<section class="w-10/12 flex flex-wrap justify-center m-auto gap-10 mb-20">
<div v-if="!characters.length" class="loading">Loading...</div>
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
      <button 
       @click="showmodal(character.id)"
       class="px-3 py-1 text-sm text-white bg-red-600 rounded-md border-0 hover:bg-red-500"
       >
         More Info
      </button>
       <p class="text-sm text-gray-700 mb-3">
         Modified:
         {{new Date(character.modified).toDateString()}}
        
      </p>
    </div>
  </div>

  <!-- MODAL DE PERSONAJES -->
  <Character
   class="modal"
   :class="{ 'is-active': modal }"
   :currentCharacter="currentCharacter"
   :modal="modal"
  />
</section>
</template>

<script>
// https://gateway.marvel.com:443/v1/public/characters/1017100?apikey=
import axios from "axios";
import Character from './Character.vue'

export default {
  components: {
    Character,
  },
  data() {
    return {
      bottom: false,
      characters: [],
      search: "",
      modal: false,
      currentCharacter: {},
    };
  },

  watch: {
    bottom(newValue) {
      if (newValue) {
        this.getData();
      }
    }
  },
  created() {
    window.addEventListener("scroll", () => {
      this.bottom = this.bottomVisible();
    });
    this.getData();
  },
  
  methods: {
    bottomVisible() {
      const scrollY = window.scrollY;
      const visible = document.documentElement.clientHeight;
      const pageHeight = document.documentElement.scrollHeight;
      const bottomOfPage = visible + scrollY >= pageHeight;
      return bottomOfPage || pageHeight < visible;
    },
    
    getData() {
      axios
        .get(
          `http://gateway.marvel.com/v1/public/characters?ts=1&apikey=5ca0254ca03b0cb4515e99240e79f903&hash=28db8be61d0ada711c2c558e79fe9d6e&limit=100&offset=100`
        )
        .then((res) => {
        this.characters = res.data.data.results;
        if (this.bottomVisible()) {
          this.getData();
        }
        })
        .catch((error) => console.log(error));
    },
    searchName() {
       axios
        .get(
          "http://gateway.marvel.com/v1/public/characters?ts=1&apikey=5ca0254ca03b0cb4515e99240e79f903&hash=28db8be61d0ada711c2c558e79fe9d6e&limit=100&offset=100"
        )
        .then((res) => {
          let allData = res.data.data.results;

          if(this.search === '') {
            this.characters = allData;
          } else {
            // Filtrar por nombre
            const names = allData.filter((data) => data.name.toLowerCase().includes(this.search))
            this.characters = names;
          }
        })
        .catch((error) => console.log(error));
    },

     fetchOne(id) {
        axios
        .get(
        `https://gateway.marvel.com:443/v1/public/characters/${id}?ts=1&apikey=5ca0254ca03b0cb4515e99240e79f903&hash=28db8be61d0ada711c2c558e79fe9d6e`
        )
        .then((res) => {
           this.currentCharacter = res.data.data.results;
           JSON.parse(JSON.stringify(this.currentCharacter))
          //  console.log(this.currentCharacter)
           this.modal = true;
        })
        .catch((error) => console.log(error));
    },
    showmodal(id) {
      this.fetchOne(id)
    },
  },
};
</script>

<style scoped>
.loading {
  color: rgb(235, 27, 27);
  text-align: center;
  font-size: 20px;
}
</style>
