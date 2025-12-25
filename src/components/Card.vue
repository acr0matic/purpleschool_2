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
    <div class="card__front">
      <div class="card__content">
        <span class="card__index">{{ formattedIndex }}</span>
        <p class="card__text">{{ words.russian }}</p>
        <p @click="emits('flip')" class="card__action">Перевернуть</p>
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
</template>

<style scoped>

</style>