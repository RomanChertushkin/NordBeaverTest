<script setup lang="ts">
import BackpackModal from '@/components/BackPack/BackpackModal.vue'
</script>

<template>
  <div class="centered bg-gradient">
    <BackpackModal />
  </div>
</template>

<style scoped>
.centered {
    min-height: 100vh;
    align-items: center;
    display: flex;
    justify-content: center;
}

.bg-gradient {
    background: linear-gradient(180deg, #85617d 0%, #6b5a5a 100%);
}
</style>
