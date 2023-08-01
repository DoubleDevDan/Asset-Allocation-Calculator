<template>
  <div class="card">
    <div class="header">
      <div
        v-if="tooltip"
        @mouseenter="showTooltip = true"
        @mouseleave="showTooltip = false"
        class="tooltip"
      >
        <span>?</span>
        <span class="tooltiptext">{{ tooltip }}</span>
      </div>
    </div>
    <div class="content">
      <slot></slot>
    </div>
    <div class="footer">
      <TheCardFooter :footer_copy="card_header" />
    </div>
    <h2 class="green"></h2>
  </div>
</template>

<script setup lang="ts">
import TheCardFooter from './TheCardFooter.vue';

defineProps<{
  card_header: string;
  tooltip: string;
}>();

let showTooltip = false;
</script>

<style scoped>
.card {
  background-color: white;
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
  height: 590px; /* Set height of card to 360px */
  width: 450px; /* Set width of card to 300px */
  display: flex;
  flex-direction: column;
}

.content {
  height: 560px; /* Set height of content to 330px */
  overflow-y: auto; /* Add scroll bar if content overflows */
  margin: 20px 10px 40px 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.header {
  height: 30px;
  text-align: right;
  padding-right: 10px;
}

.footer {
  height: 30px;
}

/* Tooltip container */
.tooltip {
  position: relative;
  display: inline-block;
  border-bottom: 1px dotted black;
  font-size: 24px;
  text-align: right;
}

/* Tooltip text */
.tooltip .tooltiptext {
  visibility: hidden;
  width: 400px;
  background-color: black;
  color: #fff;
  text-align: center;
  padding: 5px 0;
  border-radius: 6px;
  position: absolute;
  z-index: 1;
  font-size: 18px;
  padding-right: 5px;
}

/* Show the tooltip text when you mouse over the tooltip container */
.tooltip:hover .tooltiptext {
  visibility: visible;
}
</style>
