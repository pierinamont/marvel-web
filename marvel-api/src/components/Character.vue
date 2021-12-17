<template>
  <div 
  v-if="modal"
  class="container flex justify-center mx-auto">
    <button class="px-6 py-2 text-white bg-blue-600 rounded shadow-xl" type="button">
        open model</button>
    <div class="absolute inset-0 flex items-center justify-center bg-gray-700 bg-opacity-50">
        <div class="max-w-sm p-6 bg-white divide-y divide-gray-500">
            <div class="flex items-center justify-between">
                <h3 class="text-2xl">{{character.name}}</h3>
                <svg 
                @click="modal = false"
                xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none" viewBox="0 0 24 24"
                    stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>

            </div>
            <div class="mt-4">
                <p class="mb-4 text-sm">
                    {{character.description}}
                </p>
                <button 
                @click="modal = false"
                class="px-4 py-2 text-white bg-red-600 rounded">Cancel</button>
                <button class="px-4 py-2 text-white bg-green-600 rounded">Save</button>
            </div>
        </div>
    </div>
</div>
</template>

<script>

export default {
    props: {
        character: {},
        modal: "",
    } 
}
</script>

