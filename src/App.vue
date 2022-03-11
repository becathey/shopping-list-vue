<script setup>
import {ref} from 'vue'
const header = ref('Shopping List')
</script>

<template>
  <h1>{{header}}</h1>
</template>

<style>
@import './assets/base.css';

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  font-weight: normal;
}
h1 {
  color: #3d4852;
}

@media (min-width: 1024px) {
  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }
}
</style>
