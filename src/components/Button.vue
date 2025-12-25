<script setup>

</script>

<template>
  <button class="button">
    <slot></slot>
  </button>
</template>

<style lang="scss" scoped>
.button {
  padding: 16px 40px;
  border: none;
  border-radius: 100px;
  background-color: var(--blue-primary);
  color: var(--text-inverse);

  cursor: pointer;
  transition: background-color 0.3s ease;

  &:hover {
    background-color: var(--blue-hover);
  }
}
</style>