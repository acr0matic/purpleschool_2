<script setup>

import Score from "@/components/Score.vue";
</script>

<template>
  <div class="header">
    <div class="container">
      <div class="header__wrapper">
        <p class="header__logo">ЗАПОМНИ СЛОВО</p>
        <Score></Score>
      </div>
      <!-- /.header__wrapper -->
    </div>
  </div>
  <!-- /.container -->
</template>

<style lang="scss" scoped>
.header {
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
  width: 100%;
  padding: 24px 0;

  &__wrapper {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  &__logo {
    font-weight: 700;
    font-size: 16px;
    letter-spacing: 4px;
  }
}
</style>