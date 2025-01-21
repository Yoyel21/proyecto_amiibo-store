<template>
    <div class="cart">
        <h2>Carrito</h2>
        <ul>
            <li v-for="item in cartItems" :key="item.tail">
                {{ item.name }}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        cartItems: Array,
    },
};
</script>

<style>
.cart {
    background-color: #f9f9f9;
    padding: 20px;
    border: 1px solid #ddd;
}
</style>