<template>
    <div class="border-solid border-1 w-40">
        <img :src="amiibo.image" :alt="amiibo.name" />
        <h3>{{ amiibo.name }}</h3>
        <button @click="$emit('addToCart', amiibo)">Añadir al Carrito</button>
    </div>
    <div>
        <div class="group overflow-hidden relative shadow-lg max-w-xs">
            <a href="#" class="absolute z-10 top-0 bottom-0 left-0 right-0"></a>
            <img class="block group-hover:opacity-40 transition-opacity duration-700"
                src="https://cdn.cloudflare.steamstatic.com/steam/apps/230410/hero_capsule.jpg?t=1637183731" />
            <div
                class="absolute flex items-center group-hover:-top-0 group-hover:opacity-100 duration-700 top-full right-0 w-full opacity-0 h-1/2 transition-all">
                <img :src="amiibo.image" :alt="amiibo.name" />
            </div>
            <div class="absolute  bg-gradient-to-br duration-700 from-green-800 to-blue-800 text-white block left-0 right-0 top-full text-base h-1/2 w-full opacity-50 
    transition-all group-hover:top-1/2 group-hover:opacity-100">
                <div class="py-4 text-xs px-7">
                    <div class="text-xl font-bold">{{ amiibo.name }}</div>
                    <div class="overflow-ellipsis overflow-hidden whitespace-nowrap">
                        <span class="uppercase text-gray-400 whitespace-nowrap text-xs md:text-sm">Amiibo series: </span>
                        <span class="whitespace-nowrap overflow-hidden overflow-ellipsis relative z-20">
                            <a href="https://store.steampowered.com/developer/DigitalExtremes?snr=1_4_600__629">{{amiibo.amiiboSeries}}
                                Extremes</a> </span>
                    </div>
                    <div class="whitespace-nowrap overflow-hidden overflow-ellipsis relative z-20">
                        <span class="uppercase text-gray-400 whitespace-nowrap text-xs md:text-sm">Publisher:</span>
                        <span class="whitespace-nowrap overflow-hidden overflow-ellipsis relative z-20">
                            <a href="https://store.steampowered.com/publisher/DigitalExtremes?snr=1_4_600__629">Digital
                                Extremes</a> </span>
                    </div>
                    <div class="whitespace-nowrap overflow-hidden overflow-ellipsis relative z-20">
                        <span class="uppercase text-gray-400 whitespace-nowrap text-xs md:text-sm">All Reviews:</span>
                        <span class="whitespace-nowrap overflow-hidden overflow-ellipsis relative z-20">
                            <span class="text-positive">
                                Very Positive </span>
                            <span class="text-gray-300">(2,912)</span>
                        </span>
                    </div>
                </div>
                <div class="absolute left-0  pl-7 pt-1">
                    <button href="https://store.steampowered.com/app/230410/Warframe/"
                        class="px-4 text-base block text-green-300 rounded-sm border-2 border-opacity-20 bg-gradient-to-b duration-700 from-green-400 to-green-800">
                        Añadir al carrito
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        amiibo: Object,
    },
};
</script>

<style>
/* .amiibo-card {
    border: 1px solid #ccc;
    padding: 10px;
    text-align: center;
}

.amiibo-card img{
    width: 150px;
} */
</style>