<template>
  <div class="wrapper">
    <s-button
      v-show="!start"
      @click="
        start = true;
        setCards();
      "
      >Start
    </s-button>
    <div class="inner">
      <img
        id="avatar"
        :src="'https://robohash.org/' + hero.name"
        alt=""
        @drop="drop"
        @dragover.prevent
      />
      {{ hero.name }}{{ hero.health }}
    </div>

    <cards v-show="start" :cards="data" @drop-card="selectCard" />
  </div>
</template>
<script lang="ts" setup>
import SButton from "~/components/s-button.vue";
import axios from "axios";
import Cards from "~/components/cards.vue";

const filtredCard = ref(null);
const data = ref([]);
const hero = ref(null);
const start = ref(false);

async function setCards() {
  const options = {
    method: "GET",
    url: "https://omgvamp-hearthstone-v1.p.rapidapi.com/cards/sets/Naxxramas",
    params: { locale: "ruRU" },
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
          console.log(element);
          return element;
        }
      });
      for (let i = 0; i < 3; i++) {
        data.value.push(
          filtredCard.value[randomInteger(0, filtredCard.value.length - 1)]
        );
      }
    }
  } catch (error) {
    console.error(error);
  }
}

const optionsHero = {
  method: "GET",
  url: "https://omgvamp-hearthstone-v1.p.rapidapi.com/cards/types/Hero",
  params: { health: "30", locale: "ruRU" },
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

function drop(event) {
  hero.value.health = hero.value.health - selectedCard.value.attack;
}
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  padding: 3rem;
  position: fixed;
  height: 100%;
}
</style>