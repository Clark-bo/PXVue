<script>
import { ref, computed } from 'vue';
import TodoList from './components/TodoList.vue';
export default {
  
  name: 'App',
  components: {
    TodoList
  },
  setup() {
    const todoItems = ref([]);

    const totalItems = computed(() => todoItems.value.length);

    const completedTasks = computed(() => {
      return todoItems.value.filter(item => item.done).length;
    });

    const progress = computed(() => {
      if (totalItems.value === 0) return 0;
      return (completedTasks.value / totalItems.value) * 100;
    });

    const addItem = newItem => {
      todoItems.value.push(newItem);
    };

    const updateItem = (updatedItem, index) => {
      todoItems.value.splice(index, 1, updatedItem);
    };

    const removeItem = index => {
      todoItems.value.splice(index, 1);
    };

    return {
      todoItems,
      totalItems,
      completedTasks,
      progress,
      addItem,
      updateItem,
      removeItem
    };
  }
};
</script>

<template>
  <div class="app">
    <h1>Todo List</h1>
    <TodoList :items="todoItems" @add="addItem" @update="updateItem" @remove="removeItem" />
    <p>Total de Elementos: {{ totalItems }}</p>
    <p>Tareas Completadas: {{ completedTasks }}</p>
    <p>Progreso: {{ progress }}%</p>
  </div>
</template>

<style scoped>
  .app {
    text-align: center;
    }
    
</style>