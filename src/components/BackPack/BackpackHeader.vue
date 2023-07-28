<template>
  <div class="backpack-header">
    <div class="backpack-header__tab backpack_tab active">BACKPACK</div>
    <div class="backpack-header__tab nexus_tab inactive">NEXUS</div>
    <div class="backpack-header__tab close_tab active">
        <img src="@/assets/icons/times.svg" alt="close" />
    </div>
  </div>
</template>

<script setup lang="ts"></script>

<style scoped>
.backpack-header {
  width: 100%;
  height: 7%;
  display: flex;
}

.backpack-header__tab {
    border: 1px solid #000;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    font-style: normal;
    font-family: "Archivo";
    font-weight: 400;
    line-height: normal;
    text-transform: uppercase;
}

.backpack_tab {
width: 249px;
}

.nexus_tab {
width: 257px;
}

.close_tab {
width: 56px;
}

.active {
  background: #242223;
  color: #FFFFFF
}

.inactive {
  background: #393839;
  color: rgba(255, 255, 255, 0.47)
}

</style>
