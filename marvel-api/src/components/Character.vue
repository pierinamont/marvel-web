<template>
    <div 
    v-if="modal"
    class="flex justify-center mx-auto h-max">
        <div class="absolute inset-0 flex items-center justify-center bg-gray-700 bg-opacity-50">
            <div class="max-w-sm p-6 bg-white divide-y divide-gray-500 rounded-md">
                <div class="flex items-center justify-between">
                    <h3 class="text-2xl">{{currentCharacter[0].name}}</h3>
                    <span
                    @click="modal = false"
                    class="cursor-pointer"
                    >
                    x
                    </span>

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

