<!-- src/App.vue -->
<template>
  <div class="app">
    <TodoList />
  </div>
</template>

<script setup>
import TodoList from './components/TodoList.vue';
</script>

<style>
.app {
  font-family: 'Arial', sans-serif;
  background-color: #f0f0f0;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

@media (max-width: 600px) {
  .app {
    padding: 10px;
  }
}
</style>
