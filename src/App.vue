<template>
  <div id="app" class="container mt-5">
    <h1>My Shop</h1>
    <p class="animated fadeInRight">Take a look at our offerings below</p>
    <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
    <price value="4.52"></price>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import Price from "./components/Price.vue";

export default {
  name: "app",
  components: {
    FontAwesomeIcon,
    Price
  }
};
</script>