<template>
  <span>{{ value | currencyFormat(prefix, precision) }}</span>
</template>

<script>
export default {
  name: "price",
  props: {
    value: Number,
    prefix: {
      type: String,
      default: "Rp",
    },
    precision: {
      type: Number,
      default: 2,
    },
  },
  filters: {
    currencyFormat: function (value, prefix, precision) {
      return prefix + Number.parseFloat(value).toFixed(precision);
    },
  },
};
</script>
