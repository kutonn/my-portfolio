<template>
  <div id="app">
    <NavBar />
    <main>
      <router-view />
    </main>
    <Footer />
  </div>
</template>

<script setup>
import NavBar from './components/NavBar.vue'
import Footer from './components/Footer.vue'
</script>

<style>
* { margin: 0; padding: 0; box-sizing: border-box; }
body { 
  font-family: 'Inter', sans-serif; 
  line-height: 1.6; 
  overflow-x: hidden;
}
#app { min-height: 100vh; }
</style>