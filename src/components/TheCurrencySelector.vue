<template>
  <select
    :value="selectedCurrency"
    @input="$emit('update:selectedCurrency', $event.target?.value)"
    class="form-control"
  >
    <option v-for="currency in currencies" :value="currency">
      {{ currency }}
    </option>
  </select>
</template>

<script lang="ts">
export default {
  props: {
    currencies: {
      type: Array,
      required: true,
      default: () => ['BTC', 'ETH', 'USD'],
    },
    selectedCurrency: {
      type: String,
      required: true,
    },
  },
};
</script>
