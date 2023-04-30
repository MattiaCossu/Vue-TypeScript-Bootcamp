<script setup lang="ts">
import { reactive } from 'vue'
import Counter from './components/Counter.vue'

// define the type of the appInfo object
interface AppInfo {
  name: string
  slogan: string
}

// create a reactive object with the AppInfo type
const appInfo: AppInfo = reactive({
  name: 'Counter',
  slogan: 'an app you can count on'
})
</script>

<template>
  <div>
    <h1>{{ appInfo.name }}</h1>
    <h2>{{ appInfo.slogan }}</h2>
  </div>
  <Counter 
    :limit="10"
  >
  </Counter>
</template>