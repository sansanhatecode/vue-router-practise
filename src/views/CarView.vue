<script setup>
import { useRoute } from "vue-router"
import { ref, onBeforeMount } from "vue"
import cars from "../data.json"

const car = ref(null)
const route = useRoute()
const { id } = route.params


onBeforeMount(() => {
  car.value = cars.find(car => car.id == id)
})

</script>

<template>
  <div class="container">
    <div v-if="car">
      <h1>The Car</h1>
      <p>Make: {{ car.make }}</p>
      <p>Body: {{ car.body }}</p>
      <p>Price: ${{ car.price }}</p>
      <p>Year: {{ car.year }}</p>
    </div>
    <div v-else>
      <h1>Car Not Found</h1>
    </div>
  </div>
</template>

<style scoped>
.container {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  max-width: 800px;
  margin: 0 auto
}
</style>