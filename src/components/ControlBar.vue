<script setup lang="ts">

// define the type of the props object 
const emit = defineEmits<{
    (event: 'addCount', num: number): void
    (event: 'resetCount'): void
}>()

</script>

<template>
    <p>
        <!-- emit the addCount event with the number 1 as the argument -->
        <button @click="emit('addCount', 1)">Add</button>
        <button @click="emit('resetCount')">Reset</button>
    </p>
</template>