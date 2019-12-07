<template>
    <div class="row">
        <div class="col-md-8 offset-md-2">
            <div class="jumbotron">
                <h1 class="display-4">Trade or View your Portfolio</h1>
                <p>You may Save &amp; Load your Data</p>
                <p>Click on 'End Day' to begin a new day</p>
                <hr class="my-4">
                <h4>Your Funds is {{ funds }}</h4>
                <router-link to='/stocks'>
                    <button class="btn btn-info btn-lg mt-3">Start Trading</button>
                </router-link>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    computed: {
        funds() {
            return this.$store.getters.funds
        }
    }
}
</script>