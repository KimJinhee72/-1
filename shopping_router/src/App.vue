<script setup>
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';
</script>
<template>
  <div class="wrap">
    <Header/>
    <main>  
      <router-view></router-view>
    </main>
    <Footer/>
  </div>
</template>
<style lang="scss" scoped>
</style>