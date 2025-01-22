<template>
  <div class="fixed top-3 left-4 z-10">
    <button class="absolute left-0 p-2 rounded-3xl w-12 h-12 bg-white border-none outline-none focus:ring-0 hover:ring-0 mt-3 ml-2" @click="showCart">
      <img src="../public/shopping_cart.png" alt="See Cart" class="w-full h-full object-cover">
    </button>
  </div>
  <h1 class="text-slate-800 mb-12">Amiibo Land</h1>
  <div class="flex flex-wrap gap-5">
    <AmiiboCard v-for="amiibo in amiibos" :key="amiibo.tail" :amiibo="amiibo" @addToCart="addToCart" />
  </div>
  <Cart v-if="cartVisible" :cartItems="cartItems" />
</template>

<script>
import AmiiboCard from "./components/AmiiboCard.vue";
import Cart from "./components/Cart.vue";

export default {
  components: { AmiiboCard, Cart },
  data() {
    return {
      amiibos: [],
      cartItems: JSON.parse(localStorage.getItem("cart")) || [],
      cartVisible: false,
    };
  },
  methods: {
    fetchAmiibos() {
      fetch("https://www.amiiboapi.com/api/amiibo/")
        .then((response) => response.json())
        .then((data) => (this.amiibos = data.amiibo));
    },
    addToCart(amiibo) {
      this.cartItems.push(amiibo);
      localStorage.setItem("cart", JSON.stringify(this.cartItems));
    },
    showCart() {
      this.cartVisible = !this.cartVisible;
    },
  },
  created() {
    this.fetchAmiibos();
  },
};
</script>