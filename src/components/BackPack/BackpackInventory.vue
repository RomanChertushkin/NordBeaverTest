<template>
  <div class="backpack-inventory">
    <div
      v-for="(item, index) in renderItems"
      :key="index"
      @mousemove="showTooltip($event, item?.name)"
      @mouseleave="hideTooltip()"
      class="backpack-inventory__conatainer"
    >
      <div
        class="backpack-inventory__item"
        :class="{
          'backpack-inventory__item__blue__gradient':
            item?.type === 'weapon' && !loading,
          'backpack-inventory__item__violet__gradient':
            item?.type === 'armor' && !loading,
          'backpack-inventory__item__opacity':
            item?.cooldown && item?.count > 0 && !loading,
        }"
      >
        <div
          class="backpack-inventory__item__charges"
          v-if="item?.charges && !loading"
        >
          <img src="@/assets/icons/item-conor.svg" alt="close" />
          <div>
            {{ item?.charges }}/{{ item?.maxCharges }} {{ item?.cooldown }}
          </div>
        </div>

        <div
          class="backpack-inventory__item__iamge__wrapper"
          v-if="item?.imageUrl && !loading"
        >
          <img
            :src="item?.imageUrl"
            class="backpack-inventory__item__iamge__img"
          />
        </div>

        <div
          class="backpack-inventory__item__count"
          v-if="item?.count && !loading"
        >
          {{ item?.count }}
        </div>
      </div>

      <div
        class="backpack-inventory__item__timer__wrapper"
        v-if="item?.cooldown && !loading"
      >
        <div class="backpack-inventory__item__timer">
          <img src="@/assets/icons/timer.svg" />
          <span>{{ item?.cooldown }}s</span>
        </div>
      </div>
    </div>

    <div class="backpack-inventory__item__tooltip" ref="tooltip">
      {{ tooltipItemname }}
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, defineProps, computed, watch } from "vue";
import { useRouter, useRoute } from "vue-router";

const props = defineProps({
  filter: {
    type: String,
    required: true,
  },
});

watch(
  () => props.filter,
  (newVal, oldVal) => {
    if (newVal !== oldVal) {
      loading.value = true;
      setTimeout(() => {
        loading.value = false;
      }, 1000);
    }
  }
);

let loading = ref(true);
let caseId = 1;
let items = ref([]);
let tooltip = ref(null);
let tooltipItemname = ref("");

const renderItems = computed(() => {
  if (!!items.value) {
    if (props.filter === "all") {
      return items.value;
    }

    let filterd = items.value.filter((item) => item?.type === props?.filter);
    let itemsData = changeItems(filterd);

    return itemsData;
  }
});

const getItems = async () => {
  const response = await fetch(
    "https://us-central1-seven-seven-bit-inhouse-helper.cloudfunctions.net/vueDevTestTask-getInventoryState?case=" + caseId
  );
  let data = await response.json();

  // THIS IS TEST FUNCTION! DELETE THAT IN FEATURE
    data.inventory.forEach(e => {
        if (e.cooldown) {
            e.cooldown = 120
        }
    })
  //

  items.value = changeItems(data.inventory);
  
  startTimers(items.value);
  loading.value = false;
};

const changeItems = (itemsData) => {
  let minItems = 40;
  let itemsTemp = itemsData;

  console.log(itemsTemp.length < minItems);

  if (minItems > itemsTemp.length) {
    let summ = minItems - itemsTemp.length;
    itemsTemp = [...itemsTemp, ...Array.from({ length: summ })];
  } else {
    let closetNumber = findNearestNumberDivisibleBy5(itemsTemp.length);
    let summ = closetNumber - itemsTemp.length;

    if (summ % 5 != 0) {
      itemsTemp = [...itemsTemp, ...Array.from({ length: summ })];
    }
  }

  return itemsTemp;
};

const startTimers = (items) => {
  let itemsWithCooldown = items.filter((item) => item?.cooldown);

  itemsWithCooldown.forEach((item) => {
    let timer = setInterval(() => {
      item.cooldown -= 1;
    }, 1000);

    if (item.cooldown === 0) {
      clearInterval(timer);
    }
  });
};

const showTooltip = (event, name) => {
  if (!!name) {
    const mouseX = event?.clientX || 0;
    const mouseY = event?.clientY || 0;

    tooltip.value.style.display = "block";
    tooltip.value.style.left = mouseX + "px";
    tooltip.value.style.top = mouseY + 20 + "px";

    tooltipItemname.value = name || "";
  }
};

const hideTooltip = () => {
  tooltipItemname.value = "";
  tooltip.value.style.display = "none";
};

const findNearestNumberDivisibleBy5 = (number) => {
  const ceilMultipleOf5 = Math.ceil(number / 5) * 5;

  return ceilMultipleOf5;
};

onMounted(() => {
  const router = useRouter();
  const route = useRoute();

  console.log(route.query);

  if (route.query?.case == undefined) {
    //update case param
    router.replace({ name: "Index", query: { case: 1 } });
  }

  caseId = route.query?.case || 1;

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

.backpack-inventory__conatainer {
  position: relative;
  border: 1px solid #454545;
}

.backpack-inventory__item {
  position: relative;
  border: 1px solid #454545;
  width: 93px;
  height: 93px;
}

.backpack-inventory::-webkit-scrollbar {
  width: 3px;
}

.backpack-inventory::-webkit-scrollbar-thumb {
  background-color: #d9d9d9;
}

.backpack-inventory::-webkit-scrollbar-thumb:hover {
  background-color: #D9D9D;
}

.backpack-inventory__item__charges {
  position: relative;
  color: #fff;
  font-family: "JetBrainsMono";
  font-size: 16px;
  font-style: normal;
  font-weight: 500;
  line-height: normal;
  padding: 2px;
}

.backpack-inventory__item__charges div {
  position: absolute;
  padding-left: 5px;
}

.backpack-inventory__item__charges img {
  position: absolute;
}

.backpack-inventory__item__count {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 50px;
  padding-right: 5px;
  text-align-last: end;

  color: #fff;
  text-align: right;
  font-family: JetBrains Mono;
  font-size: 17px;
  font-style: normal;
  font-weight: 500;
  line-height: normal;
}

.backpack-inventory__item__iamge__wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  width: inherit;
  height: inherit;
}

.backpack-inventory__item__iamge__img {
  width: 74px;
  height: 74px;
}

.backpack-inventory__item__blue__gradient {
  background: radial-gradient(
      59.14% 59.14% at 50% 50%,
      #7f59ce 0%,
      rgba(127, 89, 206, 0) 100%
    ),
    #1a1a1a;
}

.backpack-inventory__item__violet__gradient {
  background: radial-gradient(
      59.14% 59.14% at 50% 50%,
      #367cce 0%,
      rgba(0, 95, 206, 0) 100%
    ),
    #1a1a1a;
}

.backpack-inventory__item__timer__wrapper {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 90px;
  height: inherit;
  z-index: 1;
  top: 25px;
  left: 0;
}

.backpack-inventory__item__timer {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.backpack-inventory__item__timer span {
  color: #fff;
  font-family: "Archivo";
  font-size: 15px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
}

.backpack-inventory__item__opacity {
  opacity: 0.5;
}

.backpack-inventory__item__tooltip {
  display: none;
  position: absolute;
  margin-left: 10px;
  border-radius: 0px 5px 5px 5px;
  border: 2px solid #6c6c6c;
  background: #1a1a1a;
  color: #969696;

  height: 31px;
  flex-shrink: 0;
  z-index: 2;

  padding: 0 5px;

  color: #969696;
  text-align: right;
  font-family: "Archivo";
  font-size: 16px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
  text-transform: uppercase;
  text-align: center;
}
</style>
