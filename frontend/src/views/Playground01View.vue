<template>
  <div v-if="randomElement">
    <p>{{ randomElement.joke }}</p>
    <button @click="selectRandomElement">nächster ...</button>
  </div>
  <div v-else>
    <p>Loading...</p>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import { BACKEND_URL } from '@/config'

const dataArray = ref([])
const randomElement = ref(null)

const fetchData = async () => {
  try {
    const response = await axios.get(BACKEND_URL)
    dataArray.value = response.data
    selectRandomElement()
  } catch (error) {
    console.error('Fehler beim Abrufen der Daten:', error)
  }
}

const selectRandomElement = () => {
  const length = dataArray.value.length

  if (dataArray.value.length > 0) {
    const randomIndex = Math.floor(Math.random() * dataArray.value.length)
    randomElement.value = dataArray.value[randomIndex]
  }
}

// fetchData nicht sofort ausführen, sondern erst nach 300 ms
onMounted(() => setTimeout(fetchData, 300))


</script>
