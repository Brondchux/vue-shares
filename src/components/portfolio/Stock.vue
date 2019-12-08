<template>
    <div class="col-md-4 mb-3">
        <div class="card">
            <div class="card-header">
                {{ stock.name }} || 
                <small><b>Price: {{ stock.price }}</b></small> || 
                <small><b>Quantity: {{ stock.quantity }}</b></small> 
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
                                v-model="quantity" 
                                :class="{danger: insufficientQuantity}"
                                placeholder="Quantity">
                        </div>
                    </div>
                    <div class="col-md-6">
                        <button 
                            class="btn btn-info float-right" 
                            @click="sellStock" 
                            :disabled="insufficientQuantity || quantity <= 0">
                        {{ insufficientQuantity ? 'Low Qty' : 'Sell' }}</button>
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
    data() {
        return {
            quantity: 0
        }
    },
    props: ['stock'],
    computed: {
        insufficientQuantity(){
            return this.quantity > this.stock.quantity
        }
    },
    methods: {
        sellStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity
            }
            console.log(order)
            this.$store.dispatch('sellStock', order)
            this.quantity = 0
        }
    }
}
</script>