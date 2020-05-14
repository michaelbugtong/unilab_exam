<template>
  <div id="app">
    <div id="nav">
        <router-link v-if="authenticated" to="/login" v-on:click.native="logout()" replace>Logout</router-link>
    </div>
    <router-view @authenticated="setAuthenticated" />

    <!--product v-bind:product="product"/-->
  </div>
</template>

<script> 
//import product from "./components/product";

export default {
  name: 'App',
  //components: {
    //product
  //},
  data() {
    return {
      authenticated: false,
      mockAccount: {
          username: "admin",
          password: "pass"
      },
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
    }
  },
  mounted() {
      if(!this.authenticated) {
          this.$router.replace({ name: "login" });
      }
  },
  methods: {
      setAuthenticated(status) {
          this.authenticated = status;
      },
      logout() {
          this.authenticated = false;
      }
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
