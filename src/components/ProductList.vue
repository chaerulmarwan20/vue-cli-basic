<template>
  <transition-group
    name="fade"
    tag="div"
    @beforeEnter="before"
    @enter="enter"
    @leave="leave"
  >
    <div
      class="row d-none mb-3 align-items-center"
      v-for="(item, index) in showItem"
      :key="item.id"
      :data-index="index"
    >
      <div class="col-1 m-auto">
        <button class="btn btn-info text-white" @click="$emit('add', item)">
          +
        </button>
      </div>
      <div class="col-sm-4">
        <img class="img-fluid d-block" :src="item.image" :alt="item.name" />
      </div>
      <div class="col">
        <h2 class="text-info">{{ item.name }}</h2>
        <p class="mb-0">{{ item.description }}</p>
        <div class="h5 float-right">
          <price :value="Number(item.price)"></price>
        </div>
      </div>
    </div>
  </transition-group>
</template>

<script>
import Price from "./Price.vue";

export default {
  name: "product-list",
  components: {
    Price,
  },
  props: ["products", "maximum"],
  computed: {
    showItem: function () {
      const max = this.maximum;
      return this.products.filter((item) => item.price <= max);
    },
  },
  methods: {
    before: function (e) {
      e.className = "d-none";
    },
    enter: function (e) {
      const delay = e.dataset.index * 100;
      setTimeout(() => {
        e.className =
          "row d-flex mb-3 align-items-center animate__animated animate__fadeInRight";
      }, delay);
    },
    leave: function (e) {
      const delay = e.dataset.index * 100;
      setTimeout(() => {
        e.className =
          "row d-flex mb-3 align-items-center animate__animated animate__fadeOutRight";
      }, delay);
    },
  },
};
</script>
