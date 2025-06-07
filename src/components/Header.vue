<template>
  <div class="head-container">
    <img class="logo" src="../assets/Logo_imi_horizontal.png" alt="" />
    <nav class="nav-area">
      <router-link class="nav-text" to="/">Форма</router-link>
      <router-link class="nav-text" to="/preview">Превью</router-link>
    </nav>
    <div class="nothing"></div>
  </div>
</template>

<script setup lang="ts">
</script>

<style scoped>
.logo {
  width: 175px;
  height: 32px;
}
.head-container {
  display: flex;
  justify-content: space-around;
  border-bottom: 1px solid #1111111a;
  padding: 20px 0;
}
.nav-text {
  text-decoration: none;
  font-weight: 400;
  font-size: 14px;
  line-height: 24px;
  letter-spacing: 0px;
  vertical-align: bottom;
  color: #1111117a;
}
.nav-area {
  display: flex;
  justify-content: space-between;
  width: 130px;
  margin-right: 155px;
}
@media (max-width: 768px) {
  .logo {
    display: none;
  }
  .nav-area {
    margin: 0;
    width: 310px;
  }
  .nothing {
    display: none;
  }
}
</style>