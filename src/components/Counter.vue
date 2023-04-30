<script setup lang="ts">
import { ref, onMounted } from 'vue'
import fetchCount from '../services/fetchCount'

// Verbose way:
// define the type of the props object
interface Props {
  limit: number
  alertMessageOnLimit?: string
}

// define the props object with the Props type and set default values for the props object properties 
// withDefaults is a function from the vue package that allows us to set default values for props
const props = withDefaults(defineProps<Props>(), {
    alertMessageOnLimit: 'can not go any higher'
})

// define ref for count and initialize it to null (because we don't know the value yet)
const count = ref<number | null>(null)

// fetch the count from the server when the component is mounted
onMounted(() => {
  fetchCount((initialCount) => {
    count.value = initialCount
  })
})

// define a function to add to the count
function addCount(num: number) {
  if (count.value !== null) {
    if (count.value >= props.limit) {
      alert(props.alertMessageOnLimit)
    }
    else {
      count.value += num
    }
  }
}

/* defineProps offers two ways to define the types of our props

Generic type argument:
const props = defineProps<{
  limit: number,
  alertMessageOnLimit: string
}>()

Function argument:
const props = defineProps({
  limit: { type: Number, required: true },
  alertMessageOnLimit: { type: String, required: true }
})
*/ 
</script>

<template>
  <p>{{ count }}</p>
  <p>
    <button @click="addCount(1)">Add</button>
  </p>
</template>