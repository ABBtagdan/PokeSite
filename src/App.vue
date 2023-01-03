<template>
  <center>
  <h1>{{ pokeCount }}</h1>
  <button @click="slide--; updatePokemon(prev)">previous</button>
  <button @click="slide++; updatePokemon(next)">next</button>
  <label>Shiny</label>
  <input type="checkbox" v-model="shiny" @change="updatePokemon(link)"/>
  </center>
  
  <div class = "pokemons">
    <vuePokemon style="margin: 50px;" v-for="p in pokemons" :key = pokemons.indexOf(p) :name =p.name :imgurl=p.url :isShiny="shiny" />
  </div>
  
</template>
<script setup>
import vuePokemon from "./components/vuePokemon.vue"
import {ref} from 'vue'

let shiny = ref(false)
let pokemons = ref([])
let link = "https://pokeapi.co/api/v2/pokemon?limit=50&offset=0"
let next = ""
let prev = ""
let slide = 0;
let pokeCount = ref()



function updatePokemon(l){
  
  if (l == null){ slide++; return}
  link = l
  pokemons.value = []
  fetch(l).then(res => res.json()).then(json => {pokemons.value = json.results; next = json.next; prev = json.previous; return})
  pokeCount.value = `Pokedex #${slide*50+1} - #${slide*50 + 50}`
}

updatePokemon(link)

</script>

<style>
  template{
    background-color: blue;
  }
  


  .pokemons {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    max-width: 80vw;
    flex-wrap: wrap;
    margin-left: 10vw;

  }

</style>
