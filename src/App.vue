<template>
  <div id="app" class="container mt-3">
    <navbar
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      @toggle="toggleSliderStatus"
      @delete="deleteItem"
    ></navbar>
    <h1>ARL Shop</h1>
    <price-slider
      :sliderStatus="sliderStatus"
      :maximum.sync="maximum"
    ></price-slider>
    <product-list
      :products="products"
      :maximum="maximum"
      @add="addItem"
    ></product-list>
    <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import PriceSlider from "./components/PriceSlider.vue";
import ProductList from "./components/ProductList.vue";

export default {
  name: "App",
  data: function () {
    return {
      maximum: 50,
      products: [],
      cart: [],
      sliderStatus: false,
    };
  },
  components: {
    Navbar,
    PriceSlider,
    ProductList,
  },
  computed: {
    cartTotal: function () {
      let sum = 0;
      for (const key in this.cart) {
        sum = sum + this.cart[key].product.price * this.cart[key].qty;
      }
      return sum;
    },
    cartQty: function () {
      let qty = 0;
      for (const key in this.cart) {
        qty = qty + this.cart[key].qty;
      }
      return qty;
    },
  },
  mounted: function () {
    fetch("https://hplussport.com/api/products/order/price")
      .then((res) => res.json())
      .then((data) => {
        this.products = data;
      });
  },
  methods: {
    toggleSliderStatus: function () {
      this.sliderStatus = !this.sliderStatus;
    },
    addItem: function (product) {
      let productIndex;
      const productExist = this.cart.filter((item, index) => {
        if (Number(item.product.id) === Number(product.id)) {
          productIndex = index;
          return true;
        } else return false;
      });
      if (productExist.length) this.cart[productIndex].qty++;
      else this.cart.push({ product, qty: 1 });
    },
    deleteItem: function (key) {
      if (this.cart[key].qty > 1) this.cart[key].qty--;
      else this.cart.splice(key, 1);
    },
  },
};
</script>
