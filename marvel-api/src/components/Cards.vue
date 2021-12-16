<template>
  <div
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
      src="https://flowbite.com/docs/images/blog/image-1.jpg"
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
        character
      </h5>

      <p class="text-sm text-gray-700 mb-3">
        Here are the biggest enterprise technology acquisitions of 2021 so far.
      </p>
    </div>
  </div>
</template>

<script>
// https://gateway.marvel.com:443/v1/public/characters?apikey=5ca0254ca03b0cb4515e99240e79f903

// public key: 5ca0254ca03b0cb4515e99240e79f903
// private key: a1040b26aba64a020345260eda8e56927141a512
// ts : 1
// 1a1040b26aba64a020345260eda8e56927141a5125ca0254ca03b0cb4515e99240e79f903

// 1a1040b26aba64a020345260eda8e56927141a5125ca0254ca03b0cb4515e99240e79f903
// hash: 28db8be61d0ada711c2c558e79fe9d6e
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
          "http://gateway.marvel.com/v1/public/comics?ts=1&apikey=5ca0254ca03b0cb4515e99240e79f903&hash=28db8be61d0ada711c2c558e79fe9d6e"
        )
        .then((res) => {
          console.log(res.data);
        })
        .catch((error) => console.log(error));
    },
  },
};
</script>
