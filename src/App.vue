<script setup lang="ts">
import { ref, reactive, onMounted, computed } from 'vue'
import fetchCount from './services/fetchCount.ts' // a mock fetch function

// beyond type inference, you can also explicitly declare the type of a variable
interface appInfo {
  name: string
  slogan: string
}

// ref data with type inference
const count = ref<number | null>(null)

//http simulation
onMounted(() => {
  fetchCount((initialCount: number) => {
    count.value = initialCount
  })
})

//reactive data
const appInfo: appInfo = reactive({
  name: 'Counter',
  slogan: 'an app you can count on'
})

// define a function
function addCount(num: number) {
  if (count.value !== null) {
    count.value += num
  }
}

// computed data with type inference
const nextCount = computed(() => {
  if (count.value !== null) {
    return count.value + 1
  }
  return null
})

</script>

<template>
  <div>
    <h1>{{ appInfo.name }}</h1>
    <h2>{{ appInfo.slogan }}</h2>
  </div>
  <p>Count is: {{ count }}</p>
  <p>
    <button @click="addCount(1)">Add</button>
  </p>
</template>