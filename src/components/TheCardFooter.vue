<template>
  <div class="heading" :style="{ backgroundColor: bgColor }">
    <div class="icon">
      <img
        alt="Vue logo"
        class="logo"
        src="./../assets/logo.png"
        width="50"
        height="50"
      />
    </div>
    <div class="text">
      <h2>{{ footer_copy }}</h2>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps({
  footer_copy: {
    type: String,
    required: true,
  },
  bgColor: {
    type: String,
    default: '#00A66C',
  },
});
</script>

<style scoped>
.heading {
  display: flex;
  align-items: center;
  justify-content: space-between;
  text-align: center;
  padding: 10px;
}

.icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  background-color: transparent; /* Set background color of icon to transparent */
}

.text {
  flex: 1;
  margin-left: 10px;
}
</style>
