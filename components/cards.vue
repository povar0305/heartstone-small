<script lang="ts" setup>
const props = defineProps<{
  cards: any;
}>();
const emit = defineEmits<{
  (e: "dropCard", card: any): void;
}>();

function drag(card) {
  emit("dropCard", card);
}

import { VueDraggableNext } from "vue-draggable-next";
</script>

<template>
  <div class="cards">
    <vue-draggable-next
      v-for="card in props.cards"
      :key="card.cardId"
      :list="props.cards"
      class="card"
      draggable="true"
      @drag="drag(card)"
    >
      <img :src="card.img" />
    </vue-draggable-next>
  </div>
</template>

<style scoped>
.cards {
  display: flex;
  gap: 10px;
  justify-content: center;
  width: 100%;

  .card {
    cursor: pointer;
    transition: 0.1s ease-in-out;

    &:hover {
      transform: scale(1.1);
    }
  }
}
</style>