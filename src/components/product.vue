<template>
    <div>
        <h1>Product</h1>
        <button @click="addProduct()" >Add Product</button>
        <div v-for="list in product" v-bind:key="list.id">
            <productItem v-bind:list="list" v-on:del-prod="$emit('del-prod', list.id)"/>
        </div>
        <productModal 
            v-show="isModalVisible" 
            @close="closeModal" 
            v-on:add-prod="addProd"/>
    </div>
</template>

<script>
import productItem from "./productItem.vue";
import productModal from "./productModal.vue";

export default {
    name: "Product",
    components: {
        productItem,
        productModal
    },
    data () {
      return {
        isModalVisible: false,
      };
    },
    methods: {
        addProduct() {
            this.isModalVisible = true;
        },
        closeModal() {
            this.isModalVisible = false;
        },
        addProd(value) {
            console.log(value);
            this.$emit('add-prod', value);
        }
    },
    props: ["product"]
}
</script>

<style scoped>

</style>