<script setup>
import Button from "@/components/Button.vue";
import Header from "@/components/global/Header.vue";
import {ref} from "vue";
import Card from "@/components/Card.vue";

const score = ref(0);
const data = ref([
  {
    english: 'Door',
    russian: 'Дверь',
    state: 'opened',
    status: 'pending',
  }
])

</script>

<template>
  <Header :score></Header>
  <Button>
    Начать игру
  </Button>

  <Card :words="data[0]"></Card>
</template>

<style scoped>

</style>
