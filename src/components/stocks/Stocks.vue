<template>
    <div class="container">
        <div class="row">
            <app-stock v-for="(stock, index) in stocks" :key="index" :stock="stock"></app-stock>
        </div>
    </div>
</template>

<script>
import Stock from './Stock.vue';
export default {
    data() {
        return {
            stocks: [
                { id: 1, name: 'Google', price: 98 },
                { id: 2, name: 'Afrihub', price: 63 },
                { id: 3, name: 'Yelp', price: 78 },
                { id: 4, name: 'Linkedin', price: 23 }
            ]
        }
    },
    components: {
        appStock: Stock
    }
}
</script>