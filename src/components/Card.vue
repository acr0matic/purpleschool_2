<script setup>
import IconError from '@/assets/icons/error.svg'
import IconSuccess from '@/assets/icons/success.svg'

import {computed} from "vue";

const props = defineProps({
  index: {
    type: Number,
    default: 1,
  },
  status: {
    type: String,
    default: 'pending',
  },
  state: {
    type: String,
  },
  words: {
    type: Object,
    default: () => {
      return {
        word: 'Not defined',
        translation: 'Не задано',
      }
    }
  }
})

const isFlipped = computed(() => props.state === 'flipped')
const formattedIndex = computed(() => {
  if (props.index < 10) {
    return "0" + props.index
  }

  return props.index;
})

const emits = defineEmits(['change', 'flip'])

const updateStatus = (newStatus) => {
  emits('change', {status: newStatus});
}

</script>

<template>
  <div :class="{'card--flip': isFlipped}" class="card">
    <div class="card__wrapper">
      <div class="card__front">
        <div class="card__content">
          <p class="card__text">{{ words.word }}</p>
        </div>
        <!-- /.card__content -->

        <span class="card__index">{{ formattedIndex }}</span>
        <p class="card__action"><span @click="emits('flip')">Перевернуть</span></p>
      </div>
      <!-- /.card__front -->

      <div class="card__back">
        <div v-if="status" class="card__status">
          <IconError v-if="status === 'fail'"></IconError>
          <IconSuccess v-else-if="status === 'success'"></IconSuccess>
        </div>
        <!-- /.card__status -->

        <div class="card__content">
          <p class="card__text">{{ words.translation }}</p>
        </div>
        <!-- /.card__content -->

        <span class="card__index">{{ formattedIndex }}</span>

        <div class="card__action">
          <div v-if="status === 'pending'" class="card__select">
            <IconError @click="updateStatus('fail')"></IconError>
            <IconSuccess @click="updateStatus('success')"></IconSuccess>
          </div>

          <p v-else>Завершено</p>
        </div>
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
  perspective: -1600px;

  &--flip {
    .card__back {
      transform: rotateY(0deg);
    }

    .card__front {
      transform: rotateY(180deg);
    }
  }

  .icon-success {
    color: #09BB00;
  }

  .icon-error {
    color: #D00303;
  }

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
    transition: transform 0.4s ease;

    &::after {
      content: '';
      position: absolute;
      inset: 28px 20px 24px;

      border-radius: 12px;
      border: 1px solid #CCE8FF;
    }
  }

  &__front {
  }

  &__back {
    transform: rotateY(180deg);
  }

  &__content {
    position: relative;
    z-index: 2;
  }

  &__index,
  &__action {
    position: absolute;
    z-index: 2;
    display: inline-block;
    padding: 4px;
  }

  &__index {
    top: 16px;
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


    svg,
    span {
      transition: color 0.3s ease;
      cursor: pointer;

      &:hover {
        color: var(--blue-primary);
      }
    }
  }

  &__select {
    display: flex;
    align-items: center;
    gap: 32px;
    margin-bottom: -8px;
    padding: 4px 8px;

    svg {
      width: 24px;
      height: 24px;
    }
  }

  &__status {
    position: absolute;
    z-index: 2;
    top: 10px;
    left: 50%;
    transform: translateX(-50%);

    svg {
      width: 40px;
      height: 40px;
    }
  }
}
</style>