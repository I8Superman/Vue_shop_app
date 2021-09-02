<template>
  <b-col md="5" class="m-3">
    <div>
      <b-card header="List of products">
        <b-card-group deck>
          <!-- v-for works as .forEach and iterates through the elems in the array, creating a li elem for each, assigning a unique key identifier. 'success' and 'danger' are predefined colors from Bootstrap-->
          <b-card v-for="product in products" :border-variant="product.inventoryStatus? 'success' : 'danger'" align="center" :key="product.id">
            <b-card-text>
              <strong>{{product.name}}</strong>
            </b-card-text>
            <b-card-text>Price {{product.price}}</b-card-text>
            <b-card-text>From: {{product.brand}}</b-card-text>
            <b-card-text>{{product.inventoryStatus? 'In stock':'Not in stock'}}</b-card-text>
            <hr />
            <b-row>
              <b-col>
                <b-button variant="danger" @click="deleteProduct(product.id)">
                  <i class="fas fa-trash-alt"></i>
                </b-button>
              </b-col>
              <b-col>
                <UpdateProduct :product="product" @updateProduct="updateProduct" />
              </b-col>
            </b-row>
          </b-card>
        </b-card-group>
      </b-card>
    </div>
  </b-col>
</template>

<script>
import UpdateProduct from "./UpdateProduct.vue";
export default {
  props: ["products"], // Write the props RECIEVED/PASSED to THIS component here
  components: {
    UpdateProduct,
  },
  methods: {
    deleteProduct(productId) {
      this.$emit("deleteProduct", productId); // We emit the 'deleteProduct', with an argument of the product id
    },
    updateProduct(updatedProduct) {
      // Annoying: you have to pass the data all the way up through the parent chain to get to the root component (App.vue) to make the put request to the server
      this.$emit("updateProduct", updatedProduct);
    },
  },
};
</script>

<style>
</style>