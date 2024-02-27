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
</script>

<template>
  <div class="cards">
    <div
      v-for="card in props.cards"
      :key="card.cardId"
      class="card"
      draggable="true"
      @dragend="drag(card)"
    >
      <img :src="card.img" />
    </div>
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
