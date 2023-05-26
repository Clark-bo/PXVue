<script>
  import { ref, reactive, toRefs } from 'vue';
  import TodoListItem from './TodoListItem.vue';  
  export default {
    
    name: 'TodoList',
    components: {
      TodoListItem
    },
    props: {
      items: {
        type: Array,
        required: true
      }
    },
    setup(props, { emit }) {
      const newItem = reactive({
        title: '',
        description: '',
        done: false
      });
  
      const addItem = () => {
        if (newItem.title && newItem.description) {
          emit('add', { ...newItem });
          clearNewItem();
        }
      };
  
      const clearNewItem = () => {
        newItem.title = '';
        newItem.description = '';
        newItem.done = false;
      };
  
      const updateItem = (index, updatedItem) => {
        emit('update', updatedItem, index);
      };
  
      const removeItem = index => {
        emit('remove', index);
      };
  
      return {
        ...toRefs(newItem),
        addItem,
        updateItem,
        removeItem
      };
    }
  };
</script>

<template>
    <div class="todo-list">
      <div class="add-item">
        <input type="text" v-model="newItem.title" placeholder="Title" />
        <input type="text" v-model="newItem.description" placeholder="Description" />
        <button @click="addItem">Agregar</button>
      </div>
      <ul>
        <TodoListItem v-for="(item, index) in items" :key="index" :item="item" @update="updateItem(index, $event)" @remove="removeItem(index)" />
      </ul>
    </div>
</template>

<style scoped>
    .todo-list {
        width: 300px;
        margin: 0 auto;
        padding: 2rem;
        border: 1px solid #0c8b02;
        border-radius: 5px;
        }
</style>