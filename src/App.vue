<script setup lang="ts">
import Navbar from './components/Navbar.vue'
import MainTop from './components/MainTop.vue'
import Projects from './components/Projects.vue'
</script>

<template>
  <div class="outline">
    <div class="navbar-block">
      <Navbar/>
    </div>
    <div class="main-area">
      <MainTop/>
    </div>
    <div class="projects">
      <Projects/>
    </div>
  </div>
</template>

<style scoped lang="scss">
@import './assets/style.scss';

.outline {
  display: grid;

  grid-template-rows: 60px calc(100vh - 60px) 500px;
  grid-template-columns: 1fr;

  width: 100%;
  min-height: 100vh;
  background-color: $main-red;
  overflow-x: hidden;
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

.projects {
  width: 100%;
  height: 100%;

  grid-row: 3;
  grid-column: 1;

  margin-top: 10px;
  min-height: 0;
  overflow: hidden;

  //background-color: blue ;
}
</style>
