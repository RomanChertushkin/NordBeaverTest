<template>
  <div class="backpack-inventory">
    <div
      class="backpack-inventory__item"
      v-for="(item, index) in items"
      :key="index"
    >
      <div class="backpack-inventory__item"></div>
      {{ item?.name }}
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";

let items = ref([]);

const findNearestNumberDivisibleBy5 = (number) => {
  const ceilMultipleOf5 = Math.ceil(number / 5) * 5;

  return ceilMultipleOf5;
};

const getItems = async () => {
  // const response = await fetch('https://us-central1-seven-seven-bit-inhouse-helper.cloudfunctions.net/vueDevTestTask-getInventoryState?case=1');
  // const data = await response.json();

  const data = [
    {
      id: "3dde92f3bed87eb78a687ad06fe579661f3c8408",
      type: "misc",
      name: "Energy Dring",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/energy_potion.png?alt=media",
      count: 50,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "3dde92f3bed87eb78a687ad06fe579661f3c8408",
      type: "misc",
      name: "Energy Dring",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/energy_potion.png?alt=media",
      count: 50,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "3dde92f3bed87eb78a687ad06fe579661f3c8408",
      type: "misc",
      name: "Energy Dring",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/energy_potion.png?alt=media",
      count: 50,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "3dde92f3bed87eb78a687ad06fe579661f3c8408",
      type: "misc",
      name: "Energy Dring",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/energy_potion.png?alt=media",
      count: 50,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "3dde92f3bed87eb78a687ad06fe579661f3c8408",
      type: "misc",
      name: "Energy Dring",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/energy_potion.png?alt=media",
      count: 50,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "3dde92f3bed87eb78a687ad06fe579661f3c8408",
      type: "misc",
      name: "Energy Dring",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/energy_potion.png?alt=media",
      count: 50,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "3dde92f3bed87eb78a687ad06fe579661f3c8408",
      type: "misc",
      name: "Energy Dring",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/energy_potion.png?alt=media",
      count: 50,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "xa4b9237bachcdf19c0760cab7aec4a8359010b0",
      type: "armor",
      name: "Magic Boots",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/magic_boots.png?alt=media",
    },
    {
      id: "ea40e585fc4aba2ab50ba2e5859fa885250be57d",
      type: "misc",
      name: "Energy Dring",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/energy_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "da4b9237bacccdf19c0760cab7aec4a8359010b0",
      type: "weapon",
      name: "Double Swords",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/weapon_dark_saber_combo_icon.png?alt=media",
    },
    {
      id: "8d8b20c6a8d6f1b7bea7b701dc450488543f479a",
      type: "weapon",
      name: "Drone Weapon",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/weapon_dron_shield_icon.png?alt=media",
    },
    {
      id: "350702752173745b7ecf053d5ac7c0f3ae8c2b30",
      type: "misc",
      name: "Scroll",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/scroll.png?alt=media",
      count: 2,
    },
    {
      id: "95a2b45d0959fce61de5e695235fb8edbfebad66",
      type: "armor",
      name: "Drone Shield",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/weapon_dron_shield_icon.png?alt=media",
    },
    {
      id: "15140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 8,
      cooldown: 1690528157063,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
    {
      id: "67140a758aaeaf5f8d2a45e619c8349fc7ea91ae",
      type: "misc",
      name: "Strange Potion",
      imageUrl:
        "https://firebasestorage.googleapis.com/v0/b/seven-seven-bit-inhouse-helper.appspot.com/o/strange_potion.png?alt=media",
      count: 1,
      charges: 3,
      maxCharges: 3,
    },
  ];

  let itemsData = data;
  let minItems = 40;

  if (minItems > itemsData.length) {
    let summ = minItems - itemsData.length;

    if (summ % 5 != 0) {
      itemsData = [...itemsData, ...Array.from({ length: summ })];
    }
  } else {
    let closetNumber = findNearestNumberDivisibleBy5(itemsData.length);
    let summ = closetNumber - itemsData.length;

    console.log(closetNumber, summ);

    if (summ % 5 != 0) {
      itemsData = [...itemsData, ...Array.from({ length: summ })];
    }
  }

  items.value = itemsData;
};

onMounted(() => {
  getItems();
});
</script>

<style scoped>
.backpack-inventory {
  height: 100%;
  background: #1a1a1a;
  display: flex;
  box-sizing: border-box;
  align-content: flex-start;
  flex-wrap: wrap;
  overflow: scroll;
  overflow-x: auto;
  margin-bottom: 15px;
  margin-right: 8px;
  border: 1px solid #454545;
}

.backpack-inventory__item {
  border: 1px solid #454545;
  width: 93px;
  height: 93px;
}

.backpack-inventory::-webkit-scrollbar {
  width: 3px;
}

.backpack-inventory::-webkit-scrollbar-thumb {
  background-color: #D9D9D9;
}

.backpack-inventory::-webkit-scrollbar-thumb:hover {
  background-color: #D9D9D;
}
</style>
