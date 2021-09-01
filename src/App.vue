<template>
  <div id="app">
    <AppHeader />
    <b-container>
      <b-row class="justify-content-center">
        <AddProduct />
        <!-- We can pass data (props) to a component by simply using the v-bind directive (':' for shorthand). Here we bind the productList array to the ListProduct component and call the props 'productlist' -->
        <ListProduct :products="productList" />
      </b-row>
    </b-container>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AddProduct from "./components/AddProduct.vue";
import ListProduct from "./components/ListProduct.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    AppHeader,
    AddProduct, // Called child components
    ListProduct, // It is best to keep the state of the data in the parent component and pass them to children with props. The children should NOT mutate the props, but instead EMIT events that may change the props at the parent level (and then the changed props are sent to the child anew)
  },
  data() {
    return {
      productList: [],
    };
  },
  methods: {
    async getProductList() {
      try {
        let result = await axios.get("http://localhost:3000/products/");
        // console.log(result.data);
        this.productList = result.data;
        console.log(this.productList);
      } catch (error) {
        console.log(error);
      }
    },
  },
  mounted() {
    this.getProductList();
  },
};
</script>

<style>
</style>
