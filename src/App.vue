<script setup>
import {ref, computed} from 'vue'
const header = ref('Shopping List')
const items = ref([])
const reversedItems = computed(() => [...items.value].reverse())
const newItem = ref("")
const newItemHighPriority = ref(false)
const editing = ref(false)
const saveItem = () => {
  items.value.push({
    id: items.value.length + 1, 
    label: newItem.value, 
    highPriority: newItemHighPriority.value
  })
  newItem.value = ""
  newItemHighPriority.value = ""
}
const doEdit = (e) => {
  editing.value = e
  newItem.value = ""
  newItemHighPriority.value = ""
}
const togglePurchased = (item) => {
  item.purchased = !item.purchased
}
</script>

<template>
  <div class="header">
    <h1>{{header}}</h1>
    <button v-if="editing" @click="doEdit(false)" class="btn">Cancel</button>
    <button v-else @click="doEdit(true)" class="btn btn-primary">Add Item</button>
  </div>
  <form 
    v-if="editing"
    class="add-item-form"
    @submit.prevent="saveItem"
  >
    <input 
      v-model.trim="newItem" 
      type="text" 
      placeholder="Add an item"
    >
    <label>
      <input type="checkbox" v-model="newItemHighPriority">
      High Priority
    </label>
    <button 
      :disabled="newItem.length < 5"
      class="btn btn-primary">Save Item</button>
  </form>

  <ul>
    <li 
      v-for="(item, /* index */) in reversedItems" 
      @click="togglePurchased(item)"
      :key="item.id"
      :class="{strikeout: item.purchased, priority: item.highPriority}"
    >{{item.label}}</li>
  </ul>
  <p v-if="items.length > 0" class="click-notice">Click items to mark as purchased.</p>
  <p v-if="!items.length">List is currently empty!</p>
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
p {
  margin-top: 1rem;
}
.click-notice {
  font-style: italic;
}
.btn {
  border: none;
  border-radius: 3px;
  margin: auto 1rem;
  padding: 0.5rem 0.75rem;
  flex-shrink: 0;
  cursor: pointer;
  font-size: 0.9rem;
  letter-spacing: 0.5px;
  transition: all 0.1s ease-in;
}
.btn[disabled] {
  background: hsl(210, 10%, 60%);
}
.btn[disabled]:hover {
  background: hsl(210, 10%, 40%);
}
.btn-primary {
  background: hsl(210, 80%, 70%);
  color: #fff;
}
.btn-primary:hover {
  background: hsl(210, 70%, 50%);
}
.add-item-form, .header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.add-item-form input {
  width: 70%;
  box-sizing: border-box;
  border: 1px solid hsl(210, 30%, 90%);
  border-radius: 3px;
  color: hsl(210, 10%, 40%);
  box-shadow: 0 2px 4px 0 rgba(0,0,0,0.1);
  margin: 0.5rem 0;
  padding: 0.5rem 0.75rem;
  font-size: 1rem;
  letter-spacing: 0.5px;
}
input[type="text"] {
  margin-right: 1rem;
}
input[type="checkbox"] {
  display: inline !important;
  width: auto;
  box-shadow: none;
}
.strikeout {
  text-decoration: line-through;
  color: hsl(210, 20%, 80%);
}
.strikeout:hover {
  color: hsl(210, 10%, 60%);
}
.priority {
  color: hsl(30, 80%, 50%);
}

@media (min-width: 1024px) {
  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }
}
</style>
