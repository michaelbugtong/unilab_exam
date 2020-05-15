<template>
    <transition name="modal">
        <div class="modal-mask">
          <div class="modal-wrapper">
            <div class="modal-container">

              <div class="modal-header">
                <slot name="header">
                  Product Information
                </slot>
              </div>

              <div class="modal-body">
                <slot name="body">
                <form @submit="addProd">
                    <input type="text" v-model="name" name="name" placeholder="Add Name...">
                    <input type="text" v-model="description" name="description" placeholder="Add Description...">
                    <input type="text" v-model="category" name="category" placeholder="Add Category...">
                    <br>
                    <input type="submit" value="Add Product" class="btn">
                </form>
                </slot>
              </div>

              <div class="modal-footer">
                <slot name="footer">
                  
                  <button @click="close">
                    Cancel
                  </button>
                </slot>
              </div>
            </div>
          </div>
        </div>
      </transition>
</template>

<script>
//import uuid from 'uuid';
export default {
    name: "productModal",
    data() {
          return {
              name: "",
              description: "",
              category: ""
          }
      },
    methods: {
      close() {
        this.$emit('close');
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
          
          this.$emit('add-prod', newProd);
          this.$emit('close');
      }
    },
}
</script>

<style scoped>

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}

/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

</style>