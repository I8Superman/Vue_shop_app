<template>
  <div id="app">
    <AppHeader />
    <b-container>
      <b-row class="justify-content-center">
        <!-- We bind the addProduct emit to the component by using the v-on directive (shorthand @). The "addProduct" in white is the method called when the event is triggered -->
        <AddProduct @addProduct="addProduct" />
        <!-- We can pass data (props) to a component by simply using the v-bind directive (':' for shorthand). Here we bind the productList array to the ListProduct component and call the props 'productlist' -->
        <ListProduct :products="productList" @deleteProduct="deleteProduct" @updateProduct="updateProduct" />
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
        //console.log(this.productList);
      } catch (error) {
        console.log(error);
      }
    },
    async addProduct(newProduct) {
      await axios.post("http://localhost:3000/products/", newProduct); // We make a post request with our payload being the new product obj.
      this.getProductList(); // after posting we call getProductList to update our arr of products (getting what we posted)
    },
    async deleteProduct(productId) {
      await axios.delete(`http://localhost:3000/products/${productId}`);
      this.getProductList();
    },
    async updateProduct(updatedProduct) {
      console.log(updatedProduct);
      await axios.put(
        `http://localhost:3000/products/${updatedProduct.id}`,
        updatedProduct
      );
      this.getProductList();
    },
  },
  mounted() {
    this.getProductList();
  },
};
</script>

<style>
</style>
