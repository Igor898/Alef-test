<script setup lang="ts">
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
</script>

<template>
  <div class="wrapper">
    <Header />
    <main class="main">
      <router-view />
    </main>
    <Footer />
  </div>
</template>

<style scoped>
nav {
  padding: 1rem;
  background: #f0f0f0;
  margin-bottom: 1rem;
}
.wrapper {
  height: 100vh;
  display: flex;
  flex-direction: column;
}
.main {
  flex-grow: 1;
}
</style>
