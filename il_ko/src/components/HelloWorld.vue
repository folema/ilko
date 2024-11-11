<script setup>
import { map, tileLayer, marker } from 'leaflet';
import { onMounted, ref } from 'vue';
let tekst = ref()

onMounted (()=>{
  const leafletMap = map('kart').setView([61.229011, 7.093048], 13)
  const layer = tileLayer(
    'https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19,
    attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
    }
  ).addTo(leafletMap)
    
  leafletMap.addEventListener('click', (e)=>{
    tekst.value = e.latlng
    console.log(tekst.value)
  })
})
const mark = (grader)=>{
    marker(grader).addTo(leafletMap)
  }

defineProps({
  msg: String,
})


</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card kart" id="kart" >
    
  </div>
  <div class="skjerm">
    <h3>du har klikka på:
    </h3>
    <p>{{ tekst }}</p>
    <button @click="mark">legg til markør</button>
  </div>
 
</template>

<style scoped>
.kart{
  height: 600px;
  width: 600px;
  border: 4px solid red;
}
</style>
