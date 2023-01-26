<template>
    <div class="container">
        <InfiniteScrollWrapper class="products_list" :threshold="1" :show-more="hasMoreItems" @infinite="loadMore">
            <div v-for="(product, index) in products"
                 :key="index"
                 class="product">
                {{ product }}
            </div>
        </InfiniteScrollWrapper>
    </div>
</template>

<script>
    import InfiniteScrollWrapper from "@/components/InfiniteScrollWrapper.vue"
    import { ref } from "vue"
    export default {
        name: "App",

        components: {
            InfiniteScrollWrapper,
        },

        setup() {
            const products = ref(["Magazines", "Toothpaste", "Food"])
            const hasMoreItems = ref(true)
            const loadMore = () => {
                if (!hasMoreItems.value) {
                    return
                }

                products.value = [...products.value, "Candy", "Detergent", "Shampoo"]
                hasMoreItems.value = false
            }

            return {
                hasMoreItems,
                products,
                loadMore,
            }
        },
    }
</script>


<style lang="css">
    .container {
        max-width: 800px;
        margin: 0 auto;
        margin-top: 100px;
        border: 2px solid #181818;
    }
    .products_list .product {
        width: 100%;
        height: 200px;
        text-align: center;
        padding: 10px;
        display: flex;
        align-items: center;
        justify-content: center;
        background: floralwhite;
    }
    .products_list .product:not(:last-child) {
        border-bottom: 1px solid;
    }
</style>
