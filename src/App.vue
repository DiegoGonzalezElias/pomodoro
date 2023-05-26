<script setup>
import { RouterView } from 'vue-router'
import LateralNav from './components/LateralNav.vue';

</script>

<template>
  <div class="root">
    <LateralNav/>
    <RouterView />
  </div>
  
</template>

<style lang="scss">
.root{
  display: flex;
}
body {
  margin: 0
}  
@import url('https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@500;700&family=Hind+Vadodara:wght@300&family=Montserrat+Alternates:wght@300;400;500;600;700&display=swap');
</style>
