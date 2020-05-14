<template>
    <div>
        <h1>Product</h1>
        <button @click="addProduct()" >Add Product</button>
        <div v-for="list in product" v-bind:key="list.id">
            <productItem v-bind:list="list" v-on:del-prod="$emit('del-prod', list.id)"/>
        </div>
        <productModal v-show="isModalVisible" @close="closeModal" v-on:add-prod="$emit('add-prod')"/>
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
        name: "",
        description: "",
        category: ""
      };
    },
    methods: {
        addProduct() {
            this.isModalVisible = true;
        },
        closeModal() {
            this.isModalVisible = false;
        },
        addProd(e) {
            e.preventDefault();
            const today = new Date();
            const timestamp = today.getFullYear()+""+(today.getMonth()+1)+""+today.getDate()+""+today.getHours()+""+today.getMinutes()+""+today.getSeconds();

            const newProd = {
                id: timestamp, 
                name: this.name,
                description: this.description,
                category: this.category
            }
            console.log(newProd)
            this.$emit('add-prod', newProd);
            this.$emit('close');
      }
    },
    props: ["product"]
}
</script>

<style scoped>

</style>