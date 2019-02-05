<template>
  <div id="app" class="container mt-5">
    <router-view
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      @delete="deleteItem"
      @add="addItem"
      :sliderStatus="sliderStatus"
      :maximum.sync="maximum"
      :products="products"
      @toggle="toggleSliderStatus"
    ></router-view>
  </div>
</template>

<script>
import Products from "./components/Products.vue";
import Checkout from "./components/Checkout.vue";

export default {
  name: "app",
  components: {
    Products,
    Checkout
  },
  data: function() {
    return {
      maximum: 99,
      sliderStatus: true,
      cart: [],
      products: null
    };
  },
  computed: {
    cartTotal: function() {
      let sum = 0;
      for (let key in this.cart) {
        sum = sum + this.cart[key].product.price * this.cart[key].qty;
      }
      return sum;
    },
    cartQty: function() {
      let qty = 0;
      for (let key in this.cart) {
        qty = qty + this.cart[key].qty;
      }
      return qty;
    }
  },
  methods: {
    toggleSliderStatus: function() {
      this.sliderStatus = !this.sliderStatus;
    },
    deleteItem: function(id) {
      if (this.cart[id].qty > 1) {
        this.cart[id].qty--;
      } else {
        this.cart.splice(id, 1);
      }
    },
    addItem: function(product) {
      var whichProduct;
      var existing = this.cart.filter(function(item, index) {
        if (item.product.id == Number(product.id)) {
          whichProduct = index;
          return true;
        } else {
          return false;
        }
      });

      if (existing.length) {
        this.cart[whichProduct].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    }
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