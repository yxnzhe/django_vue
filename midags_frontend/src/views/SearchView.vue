<template>
    <div class="page-search">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">Search</h1>

                <h2 class="is-size-5 has-text-grey">Search keywords: "{{ query }}"</h2>
            </div>

            <Product
                v-for="product in products"
                v-bind:key="product.id"
                v-bind:product="product" />
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import Product from '@/components/Product'

export default {
    name: 'Search',
    data() {
        return {
            products: [],
            query: ''
        }
    },
    components: {
        Product
    },
    mounted() {
        document.title = 'Search | MiDAgS™'

        let url = window.location.search.substring(1)
        let params = new URLSearchParams(url)

        if(params.get('query')) {
            this.query = params.get('query')

            this.performSearch()
        }
    },
    methods: {
        async performSearch() {
            this.$store.commit('setIsLoading', true)

            await axios.post('/api/v1/products/search/', {'query': this.query})
            .then(response => {
                this.products = response.data
            })
            .catch(error => {
                console.log(error)
            })

            this.$store.commit('setIsLoading', false)
        }
    }
}
</script>