<template>
  <section>
    <h2>{{ title }}</h2>
    <h3>${{ price}}</h3>
    <p>{{ description}}</p>
    <router-link to="/products/p2">Product 2</router-link>
  </section>
</template>

<script>
    import {
        inject,
        computed
    } from 'vue';
    import {
        useRoute
    } from 'vue-router';
    export default {
        props: ['pid'],
        setup() {
            // Getting injected products from provide in App.vue
            const products = inject('products');

            const route = useRoute();

            const selectedProduct = computed(() =>
                // useRoute allows use to use route.params below
                products.value.find((product) => product.id === route.params.pid)
            );
            const title = computed(() => selectedProduct.value.title);
            const price = computed(() => selectedProduct.value.price);
            const description = computed(() => selectedProduct.value.description);

            return {
                title,
                price,
                products,
                description,
                selectedProduct
            };
        },
    };
</script>


<style scoped>
    section {
        margin: 3rem auto;
        max-width: 40rem;
        padding: 1rem;
        border-radius: 12px;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    }
</style>