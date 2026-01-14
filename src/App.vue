<script setup>
import {ref} from "vue";

import Button from "@/components/Button.vue";
import Header from "@/components/global/Header.vue";
import Card from "@/components/Card.vue";

const score = ref(0);
const data = ref([
  {
    word: 'Door',
    translation: 'Дверь',
    state: 'opened',
    status: 'pending',
  },
  {
    word: 'Book',
    translation: 'Книга',
    state: 'opened',
    status: 'pending',
  }
])

const isPlaying = ref(false);

</script>

<template>
  <div class="game">
    <Header :score></Header>

    <div class="game__content">
      <div class="container">
        <div v-if="isPlaying" class="game__grid">
          <Card v-for="(word, index) in data" :key="index" :words="word"></Card>
        </div>

        <Button v-else @click="isPlaying = true">
          Начать игру
        </Button>
      </div>
    </div>
  </div>

</template>

<style lang="scss" scoped>
.game {
  &__grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 60px 100px;
  }
}
</style>
