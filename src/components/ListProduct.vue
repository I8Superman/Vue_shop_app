<template>
  <b-col md="5" class="m-3">
    <div>
      <b-card header="List of products">
        <b-card-group deck>
          <!-- v-for works as .forEach and iterates through the elems in the array, creating a li elem for each, assigning a unique key identifier. 'success' and 'danger' are predefined colors from Bootstrap-->
          <b-card :border-variant="product.inventoryStatus? 'success' : 'danger'" align="center" v-for="product in products" :key="product.id">
            <b-card-text>
              <strong>{{product.name}}</strong>
            </b-card-text>
            <b-card-text>Price {{product.price}}</b-card-text>
            <b-card-text>From: {{product.brand}}</b-card-text>
            <b-card-text>{{product.inventoryStatus? 'In stock':'Not in stock'}}</b-card-text>
          </b-card>
        </b-card-group>
      </b-card>
    </div>
  </b-col>
</template>

<script>
export default {
  props: ["products"], // Write the props RECIEVED/PASSED to THIS component here
};
</script>

<style>
</style>