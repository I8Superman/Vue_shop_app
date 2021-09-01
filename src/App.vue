<template>
  <div id="app">
    <AppHeader />
    <b-container>
      <b-row class="justify-content-center">
        <AddProduct />
        <ListProduct />
      </b-row>
    </b-container>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AddProduct from "./components/AddProduct.vue";
import ListProduct from "./components/ListProduct.vue";

export default {
  name: "App",
  components: {
    AppHeader,
    AddProduct,
    ListProduct,
  },
};
</script>

<style>
</style>
