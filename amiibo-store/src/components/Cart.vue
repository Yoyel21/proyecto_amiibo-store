<template>
    <div class="fixed top-0 left-0 h-full w-64 bg-white shadow-lg transform transition-transform duration-300"
        :class="{ 'translate-x-0': cartVisible, '-translate-x-full': !cartVisible }">

        <!-- Encabezado del carrito -->
        <div class="p-4 flex justify-between bg-red-300">
            <h2 class="text-lg font-bold">Carrito de Amiibos</h2>
            <button @click="$emit('closeCart')" class="hover:text-black bg-sky-200">✖</button>
        </div>

        <!-- Contenido con scroll interno -->
        <div class="p-4 overflow-y-auto max-h-96">
            <ul v-if="groupedCart.length">
                <li v-for="(item, index) in groupedCart" :key="index" class="flex justify-between py-2 border-b">
                    <span>{{ item.name }} x{{ item.quantity }}</span>
                </li>
            </ul>
            <p v-else class="text-gray-500">No hay productos en el carrito.</p>
        </div>

        <!-- Botón de compra -->
        <div class="p-4 bg-gray-100">
            <button v-if="groupedCart.length" @click="completePurchase"
                class="w-full bg-indigo-500 text-white py-2 rounded-lg hover:bg-indigo-600">
                Completar Compra
            </button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        cartItems: Array,
        cartVisible: Boolean, // Se usa para mostrar/ocultar el carrito
    },
    computed: {
        groupedCart() {
            const grouped = {};
            this.cartItems.forEach((amiibo) => {
                if (grouped[amiibo.name]) {
                    grouped[amiibo.name].quantity++;
                } else {
                    grouped[amiibo.name] = { name: amiibo.name, quantity: 1 };
                }
            });
            return Object.values(grouped);
        },
    },
    methods: {
        completePurchase() {
            localStorage.removeItem("cart");
            this.$emit("clearCart");
            alert("Gracias por su compra");
        },
    },
};
</script>