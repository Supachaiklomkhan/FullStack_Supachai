<script setup>
import { ref } from 'vue';

const awesowe = ref('true')
</script>

<template>
    <button @click="awesome = !awesome">Submit</button>
    <h1 v-if="awesowe">You did it</h1>
</template>