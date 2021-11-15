<template>
  <nav class="navbar navbar-light bg-light">
    <div class="navbar-text ms-auto d-flex">
      <button class="btn btn-sm btn-outline-success" @click="$emit('toggle')">
        <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
      </button>
      <div class="dropdown ms-2" v-if="cart.length > 0">
        <button
          class="btn btn-success btn-sm dropdown-toggle"
          id="dropdownCart"
          data-bs-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <span class="badge bg-success">{{ cartQty }}</span>
          <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
          <price :value="Number(cartTotal)"></price>
        </button>
        <div
          class="dropdown-menu dropdown-menu-end mt-2"
          aria-labelledby="dropdownCart"
        >
          <div v-for="(item, index) in cart" :key="index">
            <div class="dropdown-item text-nowrap text-end">
              <span class="badge bg-warning align-text-top me-1">{{
                item.qty
              }}</span>
              {{ item.product.name }}
              <b
                ><price :value="Number(item.product.price * item.qty)"></price
              ></b>
              <a
                href="#"
                class="badge bg-danger text-white text-decoration-none"
                @click.stop="$emit('delete', index)"
                >-</a
              >
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import Price from "./Price.vue";

export default {
  name: "navbar",
  components: {
    FontAwesomeIcon,
    Price,
  },
  props: ["cart", "cartQty", "cartTotal"],
  filters: {
    currencyFormat: function (value) {
      return "Rp" + Number.parseFloat(value).toFixed(2);
    },
  },
};
</script>
