<template>
<div class='backpack-modal'>
  <BackpackHeader />

  <div class="backpack-modal__body">
    <BackpackFiltersMenu @change="activeFilter = $event"/>
    <div class="backpack-modal__body__inventory">
      <BackPackTitle class="backpack-modal__body__inventory_title" :title="activeFilter"></BackPackTitle>
      <BackpackInventory />
    </div>
  </div>

</div>
</template>

<script setup lang="ts">
import {ref} from 'vue';
import BackpackHeader from './BackpackHeader.vue';
import BackpackFiltersMenu from './BackpackFiltersMenu.vue';
import BackPackTitle from './BackPackTitle.vue';
import BackpackInventory from './BackpackInventory.vue';

let activeFilter = ref('All Items');
</script>

<style scoped>
.backpack-modal {
  width: 100%;
  height: 100%;
  width: 562px;
  height: 864px;
  flex-shrink: 0;
  background: #242223
}

.backpack-modal__body {
  height: 93%;
  display: flex;
}

.backpack-modal__body__inventory {
  display: flex;
  flex-direction: column;
  margin-left: 15px;
  margin-top: 13px;
  width: 100%;
}

.backpack-modal__body__inventory_title {
  margin-bottom: 10px;
}
</style>