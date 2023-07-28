<template>
  <div class="backpack-filters-menu">
    <div class="backpack-filters-menu__filter" v-for="filter in filters" :key="filter.name" @click="activeFilter = filter.name; emit('change', activeFilter );">
       <img :src="filter.iconSrc" :class="activeFilter.includes(filter.name) ? 'menu__icon__active' : 'menu__icon__inactive'"/>
    </div>
  </div>
</template>

<script setup lang="ts">
  import { ref, defineEmits } from 'vue';
  import itemsFilter from '@/assets/icons/items-filter.svg';
  import weaponFilter from '@/assets/icons/weapon-filter.svg';
  import armorFilter from '@/assets/icons/armor-filter.svg';
  import miscFilter from '@/assets/icons/misc-filter.svg';

  let activeFilter = ref('All Items');

  const emit = defineEmits(['change'])

  const filters = [
     {
      name: 'All Items',
      iconSrc: itemsFilter
    },
    {
      name: 'Weapons',
      iconSrc: weaponFilter
    },
    {
      name: 'Armor',
      iconSrc: armorFilter
    },
    {
      name: 'Misc',
      iconSrc: miscFilter
    }
  ]
</script>

<style scoped>
.backpack-filters-menu {
  height: 100%;
  width: 64px;
  background: #393839;
}

.backpack-filters-menu__filter {
  height: 55px;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.backpack-filters-menu__icon {
  width: 34px;
  height: 34px;
}

.menu__icon__inactive {
  opacity: 0.5;
}

.menu__icon__active {
  opacity: 1;
}

</style>
