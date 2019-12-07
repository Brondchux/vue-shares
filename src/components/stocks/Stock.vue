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
                            <input type="text" class="form-control" placeholder="Quantity" v-model.number="quantity">
                        </div>
                    </div>
                    <div class="col-md-6">
                        <button 
                            class="btn btn-info float-right" 
                            @click="buyStock"
                            :disabled="quantity <= 0 || !Number.isInteger(quantity)">
                        Buy</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['stock'],
    data() {
        return {
            quantity: 0
        }
    },
    methods: {
        buyStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity
            }

            console.log(order)
            this.quantity = 0
        }
    }
}
</script>