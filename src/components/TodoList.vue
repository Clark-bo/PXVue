<script>
import { ref, reactive, } from 'vue';
import TodoListItem from './TodoListItem.vue';

export default {
  components: {
    TodoListItem,
  },
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  setup(props, { emit }) {
    const newItem = reactive({
      title: '',
      description: '',
      done: false,
    });

    const addItem = () => {
      emit('add', { ...newItem });
      newItem.title = '';
      newItem.description = '';
    };

    const updateItem = (index, updatedItem) => {
      emit('update', updatedItem, index);
    };

    const removeItem = index => {
      emit('remove', index);
    };

    return {
      newItem,
      addItem,
      updateItem,
      removeItem,
    };
  },
};
</script>

<template>
  <div class="todo-list">
    <input class="form-control" v-model="newItem.title" placeholder="Título" />
    <p></p>
    <input class="form-control" v-model="newItem.description" placeholder="Descripción" />
    <p></p>
    <button class="btn btn-primary" @click="addItem">Agregar</button>
    <ul class="list-group mt-3">
      <TodoListItem v-for="(item, index) in items" :key="index" :item="item" @update="updateItem(index, $event)" @remove="removeItem(index)" />
    </ul>
  </div>
</template>

<style>
.todo-list {
  margin-bottom: 20px;
}

.todo-list input {
  margin-right: 10px;
}

.todo-list button {
  margin-left: 10px;
}
</style>