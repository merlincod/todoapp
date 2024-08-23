<!-- src/components/TodoList.vue -->
<template>
  <div class="todo-container">
    <h1>Ma Liste de Tâches</h1>
    <input
      v-model="newTodo"
      @keyup.enter="addTodo"
      placeholder="Ajouter une tâche..."
      class="todo-input"
    />
    <ul class="todo-list">
      <li v-for="(todo, index) in filteredTodos" :key="index" class="todo-item">
        <input
          type="checkbox"
          v-model="todo.completed"
          @change="toggleTodo(index)"
          class="todo-checkbox"
        />
        <span :class="{ completed: todo.completed }" class="todo-text">
          {{ todo.text }}
        </span>
        <button @click="removeTodo(index)" class="todo-remove">
          &#10005;
        </button>
      </li>
    </ul>
    <div class="todo-filters">
      <button @click="filter = 'all'" :class="{ active: filter === 'all' }">Tout</button>
      <button @click="filter = 'active'" :class="{ active: filter === 'active' }">Actives</button>
      <button @click="filter = 'completed'" :class="{ active: filter === 'completed' }">Complètes</button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const newTodo = ref('');
const todos = ref([]);
const filter = ref('all');

const filteredTodos = computed(() => {
  if (filter.value === 'active') {
    return todos.value.filter(todo => !todo.completed);
  } else if (filter.value === 'completed') {
    return todos.value.filter(todo => todo.completed);
  } else {
    return todos.value;
  }
});

function addTodo() {
  if (newTodo.value.trim()) {
    todos.value.push({ text: newTodo.value, completed: false });
    newTodo.value = '';
  }
}

function removeTodo(index) {
  todos.value.splice(index, 1);
}

function toggleTodo(index) {
  todos.value[index].completed = !todos.value[index].completed;
}
</script>

<style scoped>
.todo-container {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 8px;
  background-color: #ffffff;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
  border: 1px solid #e0e0e0;
}

h1 {
  font-size: 28px;
  color: #333;
  margin-bottom: 20px;
  text-align: center;
}

.todo-input {
  width: 100%;
  padding: 12px;
  border-radius: 4px;
  border: 1px solid #ddd;
  box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
  font-size: 16px;
  margin-bottom: 20px;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  padding: 12px;
  border-radius: 4px;
  margin-bottom: 10px;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.todo-checkbox {
  margin-right: 10px;
  transform: scale(1.2);
}

.todo-text {
  flex: 1;
  font-size: 16px;
  color: #333;
}

.completed {
  text-decoration: line-through;
  color: #999;
}

.todo-remove {
  background-color: #e57373;
  border: none;
  color: white;
  border-radius: 4px;
  padding: 8px;
  cursor: pointer;
  font-size: 18px;
  transition: background-color 0.3s;
}

.todo-remove:hover {
  background-color: #d32f2f;
}

.todo-filters {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  gap: 10px;
}

.todo-filters button {
  background-color: #e0e0e0;
  border: none;
  padding: 10px 20px;
  border-radius: 20px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s, color 0.3s;
}

.todo-filters button.active {
  background-color: #007bff;
  color: white;
}

.todo-filters button:hover {
  background-color: #bdbdbd;
}
</style>
