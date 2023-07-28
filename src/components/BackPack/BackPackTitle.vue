<template>
  <div class="backpack-title">
    {{ title }}
  </div>
</template>

<script setup lang="ts">
import { defineProps } from "vue";

const props = defineProps({
  title: {
    type: String,
    required: true,
  },
});
</script>

<style scoped>
.backpack-title {
  color: #fff;
  font-family: "Archivo";
  font-size: 20px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
  text-transform: uppercase;
}
</style>
