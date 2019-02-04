<template>
  <div id="app" class="container mt-5">
    <h1>My Shop</h1>
    <product-list :maximum="maximum" :products="products"></product-list>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import ProductList from "./components/ProductList.vue";

export default {
  name: "app",
  data: function() {
    return {
      maximum: 99,
      products: null
    };
  },
  components: {
    FontAwesomeIcon,
    ProductList
  },
  mounted: function() {
    fetch("https://hplussport.com/api/products/order/price")
      .then(response => response.json())
      .then(data => {
        this.products = data;
      });
  }
};
</script>