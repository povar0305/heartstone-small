<script lang="ts" setup>
const props = defineProps<{
  hero: any;
  attack?: number;
}>();

const emit = defineEmits<{
  (e: "drop"): void;
}>();
</script>

<template>
  <div class="hero">
    <img
      :src="'https://robohash.org/' + hero.name"
      alt=""
      class="avatar"
      @drop="$emit('drop')"
      @dragover.prevent
    />
    <div v-show="attack" class="attack">
      <div class="star" />
      <span> - {{ attack }} </span>
    </div>
    <div class="health">
      <img alt="" src="https://cdn-icons-png.flaticon.com/512/893/893529.png" />
      <span>
        {{ hero.health }}
      </span>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.hero {
  position: relative;
  display: flex;
  flex-direction: column;
  margin: auto;
  align-items: center;
  transition: 1s ease-in-out;

  .avatar {
    width: 150px;
    margin-top: -85px;
  }
}

.attack {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;

  .star {
    position: relative;
    background: goldenrod;
    clip-path: polygon(
      50% 0%,
      61% 35%,
      98% 35%,
      65% 57%,
      79% 91%,
      50% 70%,
      21% 91%,
      32% 57%,
      2% 35%,
      39% 35%
    );
    width: 120px;
    height: 120px;
  }

  span {
    position: absolute;
    color: white;
    font-weight: bold;
    font-family: "Fondamento", cursive;
    text-wrap: nowrap;
    font-size: 2rem;
  }
}

.health {
  position: absolute;
  display: flex;
  align-items: center;
  right: -20px;
  bottom: -35px;
  width: 48px;
  height: 48px;
  justify-content: center;

  img {
    position: absolute;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  span {
    width: auto;
    z-index: 2;
    color: white;
    font-weight: bold;
    font-size: 1rem;
    font-family: "Fondamento", cursive;
  }
}
</style>
