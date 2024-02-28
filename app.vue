<template>
  <div class="wrapper" :class="{ open: start }">
    <img v-if="start" class="bg" src="./assets/bg.jpg" alt="" />
    <img v-if="!start" class="bg" src="./assets/start.jpg" alt="" />
    <s-button
      v-show="!start"
      class="start-btn"
      @click="
        setCards();
      "
      >Start
    </s-button>
    <hero :attack="attack" :hero="hero"  @drop="drop" v-show="start "/>
    <cards :cards="data" @drop-card="selectCard" v-if="start"/>
  </div>
</template>
<script lang="ts" setup>
import SButton from "~/components/s-button.vue";
import axios from "axios";
import Cards from "~/components/cards.vue";
import Hero from "~/components/hero.vue"

const filtredCard = ref(null);
const data = ref([]);
const hero = ref(null);
const start = ref(false);

async function setCards() {
  const options = {
    method: "GET",
    url: "https://omgvamp-hearthstone-v1.p.rapidapi.com/cards/sets/Naxxramas",
    headers: {
      "X-RapidAPI-Key": "2f2d323d21msh038c049da977301p114873jsn1e6d7e702dec",
      "X-RapidAPI-Host": "omgvamp-hearthstone-v1.p.rapidapi.com",
    },
  };
  try {
    const response = await axios.request(options);
    if (response.data) {
      filtredCard.value = response.data.filter((element) => {
        if (element.type == "Minion") {
          return element;
        }
      });
      for (let i = 0; i < 3; i++) {
        data.value.push(
          filtredCard.value[randomInteger(0, filtredCard.value.length - 1)]
        );
      }
      start.value = !start.value;

    }
  } catch (error) {
    console.error(error);
  }
}

const optionsHero = {
  method: "GET",
  url: "https://omgvamp-hearthstone-v1.p.rapidapi.com/cards/types/Hero",
  params: { health: "30" },
  headers: {
    "X-RapidAPI-Key": "2f2d323d21msh038c049da977301p114873jsn1e6d7e702dec",
    "X-RapidAPI-Host": "omgvamp-hearthstone-v1.p.rapidapi.com",
  },
};

try {
  const responseHero = await axios.request(optionsHero);
  if (responseHero.data) {
    hero.value = responseHero.data[randomInteger(0, responseHero.data.length)];
  }
} catch (error) {
  console.error(error);
}

function randomInteger(min, max) {
  let rand = min + Math.random() * (max + 1 - min);
  return Math.floor(rand);
}

const selectedCard = ref(null);

function selectCard(card) {
  selectedCard.value = card;
}

const attack = ref(null)
function drop() {
  attack.value=selectedCard.value.attack;
  hero.value.health = hero.value.health - selectedCard.value.attack;
  setTimeout(
      ()=> {attack.value = null}
      ,500)
  data.value.splice(data.value.indexOf(selectedCard.value),1)
  data.value.push(
      filtredCard.value[randomInteger(0, filtredCard.value.length - 1)]
  )

start.value=hero.value.health>0
}
</script>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  position: fixed;
  align-items: center;
  width: 100%;
  height: 100vh;
  justify-content: center;

  &.open {
    justify-content: space-between;
  }
}

.bg {
  position: absolute;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: -1;
}


:deep() {
  .cards {
    .card:first-child {
      transform: rotateZ(-3deg);
    }

    .card:last-child {
      transform: rotateZ(3deg);
    }
  }
}

</style>

<style>
body {
  margin: 0;
}
</style>