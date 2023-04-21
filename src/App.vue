<script setup lang="ts">
import { ref, reactive, onMounted } from 'vue'
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
  fetchCount((initalCount: number) => {
    count.value = initalCount
  })
})

//reactive data
const appInfo: appInfo = reactive({
  name: 'Counter',
  slogan: 'an app you can count on'
})
</script>

<template>
  <div>
    <h1>{{ appInfo.name }}</h1>
    <h2>{{ appInfo.slogan }}</h2>
  </div>
  <p>Count is: {{ count }}</p>
</template>