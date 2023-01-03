<template>
  <div>
    <h2>{{ name }}</h2>
    <img :src="imgLink"/>
  </div>
</template>

<script setup>
import { ref, defineProps} from 'vue'

let imgLink = ref()


const props = defineProps({
  name: String,
  imgurl: String,
  isShiny: Boolean
})

if (props.isShiny) {
fetch(props.imgurl).then(res => res.json()).then(json => imgLink.value = json.sprites.front_shiny)
}
else{
fetch(props.imgurl).then(res => res.json()).then(json => imgLink.value = json.sprites.front_default)
}

</script>