<template>
  <h1>Amiibo Land</h1>
  <button @click="showCart">Ver Carrito</button>
  <br>
  <br>
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

<style>
.amiibos {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}
</style>
