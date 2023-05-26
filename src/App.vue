<script setup lang="ts">

fuction addItem(newItem: TodoItem)

fuction updateItem(newItem: TodoItem, oldItem: TodoItem)

fuction removeItem(Item: TodoItem)

</script>

<template>
  <main>
    <!-- TODO -->
    <div class="container p-3">
      <div class="row mb-4">
        <div class="col-md-6">
          <h1>Todo List</h1>
          </div>
          <div v-if="todoItems.length > 0" class="col text-end pt-3">
            <h4>{{ completedItems }} / {{ itemCount }}</h4>
            <div class="progress">
              <div>

              </div>
            </div>
          </div>
          <div v-else class="col text-end pt-3">
            <h4 class="text-muted">Empty</h4>
      </div>
    </div>
    <div class="row mt-4">
      <div class="col">
        <todo-list items="todoItems" @add="addItem" @update="updateItem" @remove="removeItem"/>
      </div>
    </div>
  </div>
</main>
</template>

<style scoped>

</style>