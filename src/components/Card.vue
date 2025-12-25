<script setup>
import {computed} from "vue";

const props = defineProps({
  index: {
    type: Number,
    default: 1,
  },
  words: {
    type: Object,
    default: () => {
      return {
        russian: 'Не задано',
        english: 'Not defined'
      }
    }
  }
})

const formattedIndex = computed(() => {
  if (props.index < 10) {
    return "0" + props.index
  }

  return props.index;
})

const emits = defineEmits(['change', 'flip'])
</script>

<template>
  <div class="card">
    <div class="card__wrapper">
      <div class="card__front">
        <div class="card__content">
          <span class="card__index">{{ formattedIndex }}</span>
          <p class="card__text">{{ words.russian }}</p>
          <p class="card__action" @click="emits('flip')">Перевернуть</p>
        </div>
        <!-- /.card__content -->
      </div>
      <!-- /.card__front -->

      <div class="card__back">
        <span class="card__count">{{ formattedIndex }}</span>
        <p class="card__text">{{ words.english }}</p>
        <p class="card__action"></p>
      </div>
      <!-- /.card__back -->
    </div>
    <!-- /.card__wrapper -->
  </div>
</template>

<style lang="scss" scoped>
.card {
  width: 300px;
  aspect-ratio: 4 / 6;
  perspective: 1600px;

  &__wrapper {
    position: relative;
    width: 100%;
    height: 100%;
    padding: 24px;

    transform-style: preserve-3d;
    transition: 1s ease;
  }

  &__front,
  &__back {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;

    overflow: hidden;
    border-radius: 15px;
    background-color: #ffffff;
    backface-visibility: hidden;

    &::after {
      content: '';
      position: absolute;
      inset: 24px;

      border-radius: 12px;
      border: 1px solid #CCE8FF;
    }
  }

  &__count,
  &__action {
    position: absolute;
    z-index: 2;
    display: inline-block;
    padding: 4px;
  }

  &__count {
    top: 12px;
    left: 40px;

    font-size: 14px;
    background-color: var(--bg-primary);
  }

  &__action {
    left: 50%;
    bottom: 12px;
    transform: translateX(-50%);
    background-color: var(--bg-primary);

    font-weight: 700;
    font-size: 12px;
    text-transform: uppercase;
    letter-spacing: 2px;

    cursor: pointer;
    transition: color 0.3s ease;

    &:hover {
      color: var(--blue-primary);
    }
  }
}
</style>