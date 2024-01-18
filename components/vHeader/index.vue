<template>
  <header>
    <div class="logo">
      <NuxtLink :to="'/'">
      <img :src="'/img/logo.png'">
    </NuxtLink>
    </div>
    <nav class="menu">
      <a>Works</a>
      <a>About</a>
    </nav>
    <div class="btn-group">
      <langBtn />
      <normalBtn>Let’s work</normalBtn>
    </div>
  </header>
</template>
  
<script setup lang="ts">
import langBtn from '@/components/UI/langBtn';
import normalBtn from '@/components/UI/normalBtn';
</script>
  
<style lang="scss" scoped>
@import 'assets/css/main.scss';

header {
  height: 121px;
  padding: 0 50px;
  display: grid;
  grid-template-columns: 3fr 2fr 1fr;
  gap: 91px;
  align-items: center;
  justify-items: center;

  .logo {
    width: 100%;

    img {
      height: 25px;
      width: 84px;
    }
  }

  .menu {
    display: flex;
    width: 154px;
    justify-content: space-between;

    a {
      all: unset;
      font-size: 20px;
      line-height: 20px;
      cursor: pointer;
    }
  }

  .btn-group {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 16px;
  }
}
</style>