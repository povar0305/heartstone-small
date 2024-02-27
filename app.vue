<template>
  <div class="wrapper">
    <s-button>Start</s-button>
  </div>
<div class="inner">
  <img class="avatar" :src="'https://robohash.org/'+data[0].name">

  {{hero}}
</div>
  <card :cards="data"/>
</template>
<script setup lang="ts">
import SButton from "~/components/s-button.vue";
import axios from 'axios'

const options = {
  method: 'GET',
  url: 'https://omgvamp-hearthstone-v1.p.rapidapi.com/cards/sets/Naxxramas',
  params: {locale: 'ruRU'},
  headers: {
    'X-RapidAPI-Key': '2f2d323d21msh038c049da977301p114873jsn1e6d7e702dec',
    'X-RapidAPI-Host': 'omgvamp-hearthstone-v1.p.rapidapi.com'
  }
};
const filtredCard=ref(null)
const data=ref([])
const hero=ref(null)


try {
  const response = await axios.request(options);
  if(response.data){
    filtredCard.value=response.data.filter((element)=>{
      if(element.type=='Minion'){
        console.log(element)
        return element
      }
    })
    for (let i = 0; i < 3; i++) {
      data.value.push(filtredCard.value[randomInteger(0,filtredCard.value.length-1)])
    }

    console.log(data.value)

  }
} catch (error) {
  console.error(error);
}



const optionsHero = {
  method: 'GET',
  url: 'https://omgvamp-hearthstone-v1.p.rapidapi.com/cards/types/Hero',
  params: {health: '30'},
  params: {locale: 'ruRU'},
  headers: {
    'X-RapidAPI-Key': '2f2d323d21msh038c049da977301p114873jsn1e6d7e702dec',
    'X-RapidAPI-Host': 'omgvamp-hearthstone-v1.p.rapidapi.com'
  }
};

try {
  const responseHero = await axios.request(optionsHero);
  if(responseHero.data){
hero.value=responseHero.data[randomInteger(0,responseHero.data.length)]
  }
} catch (error) {
  console.error(error);
}



function randomInteger(min, max) {
  let rand = min + Math.random() * (max + 1 - min);
  return Math.floor(rand);
}

</script>

<style scoped>

.wrapper{
  display: flex;
  flex-direction: column;
  padding: 3rem;
}

</style>