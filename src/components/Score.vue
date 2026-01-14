<script setup>
import IconHealth from '@/assets/icons/health.svg'

const props = defineProps({
  count: {
    type: Number,
    default: 0
  }
})
</script>

<template>
  <div class="score">
    <span>{{ count }}</span>
    <IconHealth></IconHealth>
  </div>
</template>


<style scoped>
.score {
  display: flex;
  gap: 12px;
  align-items: center;

  padding: 12px 24px;
  border-radius: 100px;

  background-color: var(--blue-secondary);
  font-weight: 700;
  color: var(--blue-primary);

  .icon-health {
    width: 16px;
    height: 16px;
  }
}

</style>