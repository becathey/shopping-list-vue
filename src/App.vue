<script setup>
import {ref} from 'vue'
const header = ref('Shopping List')
const items = ref([
  {id: 1, label: "1 lb chicken"},
  {id: 2, label: "1 potato"},
  {id: 3, label: "3 Serrano chiles"}
])
const newItem = ref("")
const newItemHighPriority = ref(false)
</script>

<template>
  <h1>{{header}}</h1>
  <input v-model.trim="newItem" type="text" placeholder="Add an item">
  <div>{{newItem}}</div>
    <label>
      <input type="checkbox" v-model="newItemHighPriority">
      High Priority
    </label>

  <ul>
    <li v-for="({id, label}, /* index */) in items" :key="id">{{label}}</li>
  </ul>
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
  color: hsl(210, 20%, 30%);
}
ul {
  list-style: none;
  padding: 0;
}
li {
  display: flex;
  align-items: center;
  line-height: 1.75;
  letter-spacing: 0.5px;
  color: hsl(210, 20%, 30%);
  font-size: 1.25rem;
  cursor: pointer;
  transition: all 0.1s ease-in;
}
li:hover {
  color: hsl(210, 10%, 10%);
}
input[type="checkbox"] {
  display: inline !important;
  width: auto;
  box-shadow: none;
}

@media (min-width: 1024px) {
  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }
}
</style>
