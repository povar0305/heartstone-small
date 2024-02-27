<script setup lang="ts">
const props = defineProps<{
  cards: any
}>()
const emit = defineEmits<{
  (e: 'dropCard', card: any): void
}>()


function drag(card){
  emit('dropCard',card)
}


</script>

<template>
  <div class="cards">
      <div class="card" v-for="card in props.cards" :key="card.cardId" draggable="true" @dragend="drag(card)">
        <img :src="card.img"/>
        {{ card }}
      </div>
  </div>
</template>

<style scoped>

</style>