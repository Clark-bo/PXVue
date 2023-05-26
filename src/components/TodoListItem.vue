<script>
import { ref, reactive, getCurrentInstance } from 'vue';

export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  setup(props) {
    const editing = ref(false);
    const editedItem = reactive({ ...props.item });

    const { emit } = getCurrentInstance();

    const editItem = () => {
      editing.value = true;
    };

    const saveItem = () => {
      editing.value = false;
      emit('update', editedItem);
    };

    const removeItem = () => {
      emit('remove');
    };

    return {
      editing,
      editedItem,
      editItem,
      saveItem,
      removeItem,
    };
  },
};
</script>



<template>
  <li class="list-group-item">
    <div class="todo-list-item">
      <input class="form-control" v-model="editedItem.title" :disabled="!editing" />
      <input class="form-control" v-model="editedItem.description" :disabled="!editing" />
      <button class="btn btn-outline-primary" @click="editItem">Editar</button>
      <button class="btn btn-outline-success" @click="saveItem" :disabled="!editing">Guardar</button>
      <button class="btn btn-outline-danger" @click="removeItem">Remover</button>
    </div>
  </li>
</template>
