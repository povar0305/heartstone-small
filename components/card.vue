<script setup lang="ts">

const props = defineProps<{
  cards: any
}>()
</script>

<template>
  <div class="cards">
    <div class="card" v-for="card in props.cards">
      <img :src="card.img"/>
      {{card}}

    </div>
  </div>
</template>

<style scoped>

</style>