<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-info mb-5">
        <router-link to="/" tag="a" class="navbar-brand" active-class="active">Stock Trader</router-link>
        
        <button @click="isToggle = !isToggle" class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" :class="{show: isToggle}" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
                <router-link to="/portfolio" tag="li" class="nav-item" active-class="active"><a class="nav-link">Portfolio</a></router-link>
                <router-link to="/stocks" tag="li" class="nav-item" active-class="active"><a class="nav-link">Stocks</a></router-link>
            </ul>
            <ul class="navbar-nav navbar-right">
                <li class="nav-item">
                    <a class="nav-link" style="cursor: pointer" @click="endDay">End Day</a>
                </li>
                <li class="nav-item dropdown" @click="isShowing = !isShowing">
                    <a 
                        class="nav-link dropdown-toggle" 
                        href="#" id="navbarDropdown" 
                        role="button" 
                        data-toggle="dropdow" 
                        aria-haspopup="true" 
                        aria-expanded="false">
                        Save &amp; Load
                    </a>
                    <div 
                        class="dropdown-menu" 
                        :class="{show: isShowing}"
                        aria-labelledby="navbarDropdown">
                        <a class="dropdown-item" href="#" @click="saveData">Save Data</a>
                        <a class="dropdown-item" href="#" @click="loadData">Load Data</a>
                    </div>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#" tabindex="-1" aria-disabled="true"><b>Funds: {{ funds | currency }}</b></a>
                </li>
            </ul>
        </div>
    </nav>
</template>

<script>
export default {
    data() {
        return {
            isShowing: false,
            isToggle: false
        }
    },
    computed: {
        funds() {
            return this.$store.getters.funds
        }
    },
    methods: {
        endDay() {
            this.$store.dispatch('randomizeStocks')
        },
        saveData() {
            const data = {
                funds: this.$store.getters.funds,
                stockPortfolio: this.$store.getters.stockPortfolio,
                stocks: this.$store.getters.stocks
            }

            this.$http.put('data.json', data)
        },
        loadData() {
            this.$store.dispatch('loadData')
        }
    }
}
</script>