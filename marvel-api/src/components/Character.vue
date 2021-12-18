<template>
    <div 
    v-if="modal"
    class="flex justify-center mx-auto h-max">
        <div class="absolute inset-0 flex items-center justify-center bg-gray-700 bg-opacity-50">
            <div class="max-w-sm p-6 bg-white divide-y divide-gray-500 rounded-md">
                <div class="flex items-center justify-between">
                    <h3 class="text-2xl">{{currentCharacter[0].name}}</h3>
                    <svg 
                    @click="modal = false"
                    xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 cursor-pointer" fill="none" viewBox="0 0 24 24"
                        stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" />
                    </svg>

                </div>
                <div class="mt-4">
                    <p
                    v-if="currentCharacter[0].description"
                    class="mt-4 mb-4 text-sm"
                    >
                    {{currentCharacter[0].description}}
                    </p>
                    <p 
                    v-else
                    class="mt-4 mb-4 text-sm"
                    >
                    {{noDescription}}
                    </p>
                    <button 
                    @click="modal = false"
                    class="px-4 py-2 text-white bg-red-600 rounded mr-9">Cancel</button>
                    <button class="px-4 py-2 text-white bg-green-600 rounded">Save</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return {
            noDescription: "There's no description",
        }
    },
    props: {
        currentCharacter: {},
        modal: "",
    },
}
</script>

