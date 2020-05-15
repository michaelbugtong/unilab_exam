<template>
    <div>

    <div class="product-item">
        <p v-on:click="editItems(list)">{{ list.name + ' | ' + list.description + ' | ' + list.category}}
            <button @click="$emit('del-prod', list.id)" class="del">x</button>
        </p>
        
    </div>
    <productModal v-show="isModalVisible" @close="closeModal"/>
    </div>
</template>

<script>

import productModal from "./productModal.vue";

export default {
    name: "productItem",
    props: ["list"],
    components: {
        productModal
    },
    data () {
      return {
        isModalVisible: false,
      };
    },
    methods: {
        editItems(item) {
            console.log(item);
            this.isModalVisible = true;
        },
        showModal() {
            this.isModalVisible = true;
        },
        closeModal() {
            this.isModalVisible = false;
        }
    }
}
</script>

<style scoped>

.product-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
  }

  .is-complete {
    text-decoration: line-through;
  }

  .product-item:hover {
    background-color: white;
    cursor: pointer;
  }

  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
  }

</style>