<template>
    <div class="col-md-4 mb-3">
        <div class="card">
            <div class="card-header">
                {{ stock.name }} || <small>Cost: <b>${{ stock.price }}</b></small>
            </div>
            <div class="card-body">
                <div class="row">
                    <div class="col-md-6">
                        <div class="input-group mb-3">
                            <div class="input-group-prepend">
                                <span class="input-group-text">?</span>
                            </div>
                            <input 
                                type="text" 
                                class="form-control" 
                                placeholder="Quantity" 
                                :class="{danger: insufficientFunds}"
                                v-model.number="quantity">
                        </div>
                    </div>
                    <div class="col-md-6">
                        <button 
                            class="btn btn-info float-right" 
                            @click="buyStock"
                            :disabled="insufficientFunds || quantity <= 0 || !Number.isInteger(quantity)">
                        {{ insufficientFunds ? 'Low Funds' : 'Buy'}}</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .danger {
        border: 3px solid red;
    }
</style>

<script>
export default {
    props: ['stock'],
    data() {
        return {
            quantity: 0
        }
    },
    computed: {
        funds() {
            return this.$store.getters.funds
        },
        insufficientFunds(){
            return this.quantity * this.stock.price > this.funds
        }
    },
    methods: {
        buyStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity
            }
            this.$store.dispatch('buyStock', order)
            this.quantity = 0
        }
    }
}
</script>