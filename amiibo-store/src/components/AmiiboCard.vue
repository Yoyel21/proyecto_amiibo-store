<template>
    <div class="bg-white p-6 rounded-lg shadow-lg hover:shadow-2xl transition-shadow duration-300 w-72">
        <img :src="amiibo.image" :alt="amiibo.name"
            class="w-56 h-56 object-cover rounded-lg mx-auto mb-4 cursor-pointer" @click="openModal" />

        <h3 class="text-xl font-semibold text-center mb-2">{{ amiibo.name }}</h3>

        <div class="text-sm text-gray-700 space-y-1">
            <div>
                <span class="font-semibold uppercase text-gray-500">Amiibo Series: </span>
                <span>{{ amiibo.amiiboSeries }}</span>
            </div>
            <div>
                <span class="font-semibold uppercase text-gray-500">Game Series: </span>
                <span>{{ amiibo.gameSeries }}</span>
            </div>
            <div>
                <span class="font-semibold uppercase text-gray-500">Type: </span>
                <span>{{ amiibo.type }}</span>
            </div>
        </div>

        <button @click="$emit('addToCart', amiibo)"
            class="mt-4 w-full py-2 px-4 text-white rounded-lg hover:bg-indigo-600 transition-colors duration-300 bg-indigo-500">
            Añadir al Carrito
        </button>

        <!-- Modal de imagen ampliada -->
        <div v-if="isModalOpen" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center z-50"
            @click="closeModal">
            <div class="relative bg-white p-4 rounded-lg max-w-4xl">
                <img :src="amiibo.image" :alt="amiibo.name" class="max-w-full max-h-96 object-contain rounded-lg" />
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        amiibo: Object,
    },
    data() {
        return {
            isModalOpen: false
        };
    },
    methods: {
        openModal() {
            this.isModalOpen = true;
        },
        closeModal() {
            this.isModalOpen = false;
        }
    }
};
</script>