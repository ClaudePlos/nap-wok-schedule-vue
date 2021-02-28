<template>
  <div class="todolist">
     <input type="text" class="todo-input" placeholder="What needs to be done?"
        v-model="newTodo" @keyup.enter="addTodo">
     <p class="todoHere">Todo list goes here:</p>
     <div v-for="todo in todos" :key="todo.id" class="todo-item">
         {{ todo.title }}
     </div>
  </div>
</template>

<script>
export default {
  name: 'todo-list',
  idForTodo: 3,
  data () {
    return {
      newTodo: '',
      todos: [{ id: 1, title: 'Finish Homework', completed: false }]
    }
  },
  methods: {
    addTodo () {
      if (this.newTodo.trim().length === 0) {
        return
      }
      this.todos.push({ id: this.idForTodo, title: this.newTodo, completed: false })
      this.newTodo = ''
      this.idForTodo++
    }
  }
}
</script>

<style>
    .todo-input {
        width: 100%;
        padding: 10px 18px;
        font-size: 18px;
        margin-bottom: 16px;
    }

    .todoHere {
        margin: 0px;
        font-size: 15px;
        text-align: left;
        padding: 10px 3px;
    }

    .todo-item {
        margin-bottom:  12px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>
