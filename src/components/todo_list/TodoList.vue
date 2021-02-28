<template>
  <div class="todolist">
     <input type="text" class="todo-input" placeholder="What needs to be done?"
        v-model="newTodo" @keyup.enter="addTodo">
     <p class="todoHere">Todo list goes here:</p>
     <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
         <div class="todo-item-left">
           <div v-if="!todo.editing" class="todo-item-label" @dblclick="editTodo(todo)">{{ todo.title }}</div>
           <input v-else type="text" class="todo-item-label" v-model="todo.title"
              @blur="doneEditTodo(todo)" @keyup.enter="doneEditTodo(todo)" @keyup.esc="cancelEditTodo(todo)" v-focus>
         </div>
         <div class="remove-item" @click="removeTodo(index)">
            &times;
          </div>
     </div>
  </div>
</template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      newTodo: '',
      beforeEditCache: '',
      idForTodo: 3,
      todos: [{ id: 1, title: 'Finish Homework', completed: false, editing: false }]
    }
  },
  directives: {
    focus: {
    // directive definition
      mounted (el) {
        el.focus()
      }
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
      console.log(this.todos)
    },
    editTodo (todo) {
      this.beforeEditCache = todo.title
      todo.editing = true
    },
    doneEditTodo (todo) {
      todo.editing = false
    },
    cancelEditTodo (todo) {
      todo.title = this.beforeEditCache
      todo.editing = false
    },
    removeTodo (index) {
      this.todos.splice(index, 1)
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

    .todo-input:focus {
      outline: 0;
    }

    .todoHere {
        margin: 0px;
        font-size: 15px;
        text-align: left;
        padding: 10px 3px;
    }

    .todo-item {
        margin-bottom:  12px;
        font-size: 24px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .remove-item {
      cursor: pointer;
      margin-left: 14px;
      font-size: 24px;
    }

    .remove-item:hover {
      color: red;
    }
</style>
