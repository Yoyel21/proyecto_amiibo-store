<template>
  <div class="relative">
    <!-- Botón para mostrar el carrito -->
    <div class="fixed top-3 left-4 z-10 transition-transform duration-300"
      :class="{ '-translate-x-full': cartVisible }">
      <button v-if="!cartVisible"
        class="absolute left-0 p-2 rounded-3xl w-12 h-12 bg-white border-none outline-none focus:ring-0 hover:ring-0 mt-3 ml-2"
        @click="showCart">
        <img src="../public/shopping_cart.png" alt="See Cart" class="w-full h-full object-cover">
      </button>
    </div>

    <h1 class="text-slate-800 mb-12">Amiibo Land</h1>

    <!-- Grid de 3 filas x 4 columnas -->
    <div class="grid grid-cols-4 gap-5">
      <AmiiboCard v-for="amiibo in paginatedAmiibos" :key="amiibo.tail" :amiibo="amiibo" @addToCart="addToCart" />
    </div>

    <!-- Paginación -->
    <div class="mt-6 flex justify-center space-x-2">
      <button @click="prevPage" :disabled="currentPage === 1"
        class="px-4 py-2 bg-red-200 rounded-lg hover:bg-red-300 disabled:opacity-50">
        ⬅️ Anterior
      </button>
      <button @click="firstPage" :disabled="currentPage === 1"
        class="px-4 py-2 bg-red-200 rounded-lg hover:bg-red-300 disabled:opacity-50">
        Primera
      </button>

      <span class="px-4 py-2 bg-indigo-500 text-white rounded-lg">Página {{ currentPage }}</span>

      <button @click="lastPage" :disabled="currentPage >= totalPages"
        class="px-4 py-2 bg-sky-200 rounded-lg hover:bg-sky-300 disabled:opacity-50">
        Última
      </button>
      <button @click="nextPage" :disabled="currentPage >= totalPages"
        class="px-4 py-2 bg-sky-200 rounded-lg hover:bg-sky-300 disabled:opacity-50">
        Siguiente ➡️
      </button>
    </div>

    <!-- Componente del carrito offcanvas -->
    <Cart :cartItems="cartItems" :cartVisible="cartVisible" @closeCart="hideCart" @clearCart="clearCart" />
  </div>
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
      currentPage: 1,
      itemsPerPage: 12, // 3 filas x 4 columnas = 12 items por página
    };
  },
  computed: {
    // Filtrar los amiibos para mostrar solo los de la página actual
    paginatedAmiibos() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      return this.amiibos.slice(start, start + this.itemsPerPage);
    },
    // Total de páginas basado en la cantidad de amiibos
    totalPages() {
      return Math.ceil(this.amiibos.length / this.itemsPerPage);
    },
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
      this.cartVisible = true;
    },
    hideCart() {
      this.cartVisible = false;
    },
    clearCart() {
      this.cartItems = [];
      localStorage.removeItem("cart");
    },
    // Paginación
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    firstPage() {
      this.currentPage = 1;
    },
    lastPage() {
      this.currentPage = this.totalPages;
    },
  },
  created() {
    this.fetchAmiibos();
  },
};
</script>