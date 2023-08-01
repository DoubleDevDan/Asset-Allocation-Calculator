<script setup lang="ts">
import TheCard from './components/TheCard.vue';
import AssetAllocationCalculatorForm from './components/AssetAllocationCalculatorForm.vue';
</script>

<template>
  <TheCard
    card_header="Asset Allocation Calculator"
    tooltip="This is a Vue form that allows the user to input their investable assets and allocate them between two options. The form includes a text input for the investable assets, a dropdown to select the currency, a range input to allocate the percentage between two options, and a submit button. The form also displays the exchange rate and allocation for each option based on the user's input. The exchange rate is fetched from the Coinbase API and the allocation is calculated based on the user's input."
  >
    <AssetAllocationCalculatorForm />
  </TheCard>
</template>

<style scoped>
@media (min-width: 1024px) {
  header {
    text-align: center;
  }
}
</style>
