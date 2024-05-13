<script setup>
import carsData from "../data.json";
import {ref, watch, onMounted} from "vue"
import {useRouter, useRoute} from "vue-router"

const router = useRouter()

const cars = ref(carsData)
const make = ref("")
const route = useRoute()

onMounted(() => {
  make.value = route.query.make || ""
})

watch(make, () => {
  if(make.value){
    if(make.value === "All") cars.value = carsData
    else {
      cars.value = carsData.filter(car => car.make === make.value)
    }
  }
})

const handleFilterCars = () => {
  router.push({
    query: {make: make.value}
  })
}
</script>


<template>
  <main class="container">
    <h1>Our cars</h1>
    <!-- v-model is a built-in directive in Vue.js that provides two-way data binding between form inputs and component data.
      It allows you to create a direct link between the input element and the component's data property, 
      so that any changes made to the input are automatically reflected in the component's data, and vice versa. -->
    <select @change="handleFilterCars" v-model="make">
      <option value="All">All</option>
      <option value="Chevrolet">Chevy</option>
      <option value="Porsche">Porsche</option>
      <option value="Audi">Audi</option>
    </select>
    <div class="cards">
      <div 
        v-for="car in cars" :key="car.id" class="card"
        @click="router.push(`/car/${car.id}`)"
      >
        <h1>{{car.make}}</h1>
        <p>${{car.price}}</p>
      </div>
    </div>
  </main>
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

.cards {
  display: flex;
  width: 1000px;
  flex-wrap: wrap;
  margin-top: 50px;
  justify-content: center;
}

.card {
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.207);
  padding: 15px;
  width: 150px;
  margin-right: 15px;
  cursor: pointer;
  margin-bottom: 20px;

}
</style>