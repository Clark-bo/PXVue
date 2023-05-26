<script>
  import { ref, reactive } from 'vue';  
  export default {
    
    name: 'TodoListItem',
    props: {
      item: {
        type: Object,
        required: true
      }
    },
    setup(props, { emit }) {
      const editing = ref(false);
      const editedItem = reactive({ ...props.item });
  
      const saveItem = () => {
        emit('update', editedItem);
        editing.value = false;
      };
  
      const removeItem = () => {
        emit('remove');
      };
  
      return {
        editing,
        editedItem,
        saveItem,
        removeItem
      };
    }
  };
</script>

<template>
    <li class="todo-list-item">
      <div v-if="!editing">
        <div class="info">
          <h3>{{ item.title }}</h3>
          <p>{{ item.description }}</p>
        </div>
        <div class="actions">
          <button @click="editing = true">Editar</button>
          <button @click="removeItem">Remover</button>
        </div>
      </div>
      <div v-else>
        <input v-model="editedItem.title" type="text" />
        <input v-model="editedItem.description" type="text" />
        <div class="actions">
          <button @click="saveItem">Guardar</button>
        </div>
      </div>
    </li>
</template>

<style scoped>
    button{
        border: none;
        background: none;
        color: #408aeb;
        font-size: 16px;
        padding: 5px;
        cursor: pointer;
        margin-left: 5px;
    }

</style>