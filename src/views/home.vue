<template>
    <div id="Home">
        <product 
            v-bind:product="product" 
            v-on:del-prod="deleteItem" 
            v-on:add-prod="addProd" />
    </div>
</template>

<script>
import product from "../components/product";

    export default {
        name: 'Home',
        components: {
            product
        },
        data() {
            return {
                product: [
                {
                    id: 1,
                    name: "rice",
                    description: "desc rice",
                    category: "food"
                },
                {
                    id: 2,
                    name: "beef",
                    description: "desc beef",
                    category: "food"
                },
                {
                    id: 3,
                    name: "chicken",
                    description: "desc checken",
                    category: "food"
                }
            ]
            };
        },
        methods: {
            deleteItem(id) {
                this.product = this.product.filter(list => list.id !== id)
            },
            addProd(newItem) {
                this.product = [...this.product, newItem];
            }
        }
    }
</script>

<style scoped>
    #secure {
        background-color: #FFFFFF;
        border: 1px solid #CCCCCC;
        padding: 20px;
        margin-top: 10px;
    }
</style>