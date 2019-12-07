<template>
    <div class="container">
        <div class="row">
            <app-stock v-for="(stock, index) in stocks" :key="index" :stock="stock"></app-stock>
        </div>
    </div>
</template>

<script>
import Stock from './Stock'

export default {
    computed: {
        stocks(){
            return this.$store.getters.stockPortfolio
        }
    },
    components: {
        appStock: Stock
    }
}
</script>