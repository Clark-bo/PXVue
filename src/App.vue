<script>
import { reactive, computed, watch } from 'vue';
import TodoList from './components/TodoList.vue';
import 'bootstrap/dist/css/bootstrap.css';

export default {
  components: {
    TodoList,
  },
  setup() {
    const todoItems = reactive([]);

    const totalItems = computed(() => todoItems.length);

    const completedTasks = computed(() => todoItems.filter(item => item.done).length);

    const progress = computed(() => (completedTasks.value / totalItems.value) * 100 || 0);

    const addItem = newItem => {
      todoItems.push(newItem);
    };

    const updateItem = (updatedItem, index) => {
      todoItems.splice(index, 1, updatedItem);
    };

    const removeItem = index => {
      todoItems.splice(index, 1);
    };

    // Observa cambios en la propiedad 'done' de cada elemento de 'todoItems'
    watch(todoItems, () => {
      // Actualiza 'completedTasks' y 'progress' en función de 'done'
      completedTasks.value = todoItems.filter(item => item.done).length;
      progress.value = (completedTasks.value / totalItems.value) * 100 || 0;
    }, { deep: true });

    return {
      todoItems,
      totalItems,
      completedTasks,
      progress,
      addItem,
      updateItem,
      removeItem,
    };
  },
};
</script>

<template>
 <div class="app">
  <div class="background-image">
    <h1 class="text-center text-primary mt-5">- ToDo Lista -</h1>
    <div class="container mt-5">
      <div class="row">
        <div class="col-md-8 offset-md-2">
          <TodoList :items="todoItems" @add="addItem" @update="updateItem" @remove="removeItem" />
          <div class="mt-3">
            <p class="mb-1"><strong>Complementos Totales:</strong> {{ totalItems }}</p>
            <p class="mb-1"><strong>Tareas Completadas:</strong> {{ completedTasks }}</p>
            <div class="progress mt-3">
              <div class="progress-bar progress-bar-striped progress-bar-animated bg-success" role="progressbar" :style="{ width: progress + '%' }"></div>
            </div>
            <p class="mb-0"><strong>Progreso:</strong> {{ progress.toFixed(2) }}%</p>
          </div>
        </div>
      </div>
    </div>
  </div>
  </div>
</template>

<style scoped>
.app {
  background-color: #ffffff;
  padding: 20px;
}

.container {
  background-color: transparent;
  border-radius: 5px;
  padding: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.progress-bar {
  transition: width 0.3s ease-in-out;
}
.background-image {
  background-image: url('public/favicon.ico');
  background-size: fixed;
  background-position: fixed;
  background-repeat: no-repeat;
  background-attachment: fixed;
  height: 100vh;

}

</style>
