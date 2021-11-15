<template>
  <transition
    name="custom"
    enter-active-class="animate__animated animate__fadeInDown"
    leave-active-class="animate__animated animate__slideOutRight"
  >
    <div v-if="sliderStatus">
      <div class="align-items-center" :class="sliderState">
        <label for="max" class="fw-bold me-2">Max</label>
        <input
          type="number"
          name="max"
          id="max"
          class="form-control mx-2"
          style="width: 60px; text-align: center"
          v-model="maxAmount"
          @change="$emit('update:maximum', Number(maxAmount))"
        />
        <input
          type="range"
          class="form-range"
          name="max"
          min="0"
          v-model="maxAmount"
          @input="$emit('update:maximum', Number(maxAmount))"
        />
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "price-slider",
  data: function () {
    return {
      maxAmount: 50,
    };
  },
  props: ["sliderStatus", "maximum"],
  computed: {
    sliderState: function () {
      return this.sliderStatus ? "d-flex" : "d-none";
    },
  },
};
</script>

<style>
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 1s ease-in-out;
}
</style>
