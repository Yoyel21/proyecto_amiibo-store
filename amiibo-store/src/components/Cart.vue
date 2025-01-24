<template>
    <div class="bg-orange-50">
        <h1 class="text-3xl">Cart</h1>
        <ul>
            <li v-for="item in cartItems" :key="item.tail">
                {{ item.name }}
                <ul>
                    <li>{{ item.amiiboSeries }}</li>
                    <li>{{ item.gameSeries }}</li>
                </ul>
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