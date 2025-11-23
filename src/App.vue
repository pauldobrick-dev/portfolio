<script setup lang="ts">
import Navbar from './components/Navbar.vue';
import MainTop from './components/MainTop.vue'
</script>

<template>
  <div class="outline">
    <div class="navbar-block">
      <Navbar/>
    </div>
    <div class="main-area">
      <MainTop/>
    </div>
  </div>
</template>

<style scoped lang="scss">
@import './assets/style.scss';

.outline {
  display: grid;

  grid-template-rows: 60px 1fr;
  grid-template-columns: 1fr;

  width: 100vw;
  height: 100vh;
  background-color: $main-red;
}

.navbar-block {
  grid-row: 1;
  grid-column: 1;

  width: 100%;
  height: 100%;
}

.main-area {
  width: 100%;
  height: 100%;

  grid-row: 2;
  grid-column: 1;

  margin-top: 10px;
}

</style>
