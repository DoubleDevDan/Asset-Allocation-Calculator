<template>
  <div class="card">
    <div class="content">
      <TheCardContent />
    </div>
    <div class="footer">
      <TheCardFooter :footer_copy="card_header" />
    </div>
    <h2 class="green"></h2>
  </div>
</template>

<script setup lang="ts">
import TheCardFooter from './TheCardFooter.vue';
import TheCardContent from './TheCardContent.vue';

defineProps<{
  card_header: string;
}>();
</script>

<style scoped>
.card {
  background-color: white;
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
  height: 500px; /* Set height of card to 360px */
  width: 600px; /* Set width of card to 300px */
  display: flex;
  flex-direction: column;
}

.content {
  height: 470px; /* Set height of content to 330px */
  overflow-y: auto; /* Add scroll bar if content overflows */
}

.footer {
  height: 30px; /* Set height of footer to 30px */
}
</style>
