<template>
  <div class="todo">
    <h1>Todo</h1>
    <todo-list></todo-list>
  </div>
</template>

<script>
import TodoList from '@/components/todo_list/TodoList.vue'

export default {
  name: 'Todo',
  components: {
    TodoList
  }
}
</script>
