<template>
  <div class="todolist">
     <input type="text" class="todo-input" placeholder="What needs to be done?"
        v-model="newTodo" @keyup.enter="addTodo">
     <p class="todoHere">Todo list goes here:</p>

     <transition-group name="fade" enter-active-class="animated fadeInUp" leave-active-class="animated fadeOutDown">
     <todo-item v-for="(todo, index) in todosFiltered" :key="todo.id" :todo="todo" :index="index" @removeTodo="removeTodo">
     </todo-item>
     </transition-group>

     <div class="extra-container">
       <div><label><input type="checkbox" :checked="!anyRemaining" @change="checkAllTodos"> Check All </label></div>
       <div>{{ remaining }} items left </div>
     </div>
     <div class="extra-container">
      <div>
        <button :class="{ active : filter === 'all'}" @click="filter = 'all'">All</button>
        <button :class="{ active : filter === 'active'}" @click="filter = 'active'">Active</button>
        <button :class="{ active : filter === 'completed'}" @click="filter = 'completed'">Completed</button>
      </div>
      <div>
        <transition name="fade">
        <button v-if="showClearCompletedButton" @click="clearCompleted">Clear Completed</button>
        </transition>
      </div>
     </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem'
export default {
  name: 'todo-list',
  components: {
    TodoItem
  },
  data () {
    return {
      newTodo: '',
      beforeEditCache: '',
      idForTodo: 2,
      filter: 'all',
      todos: [{ id: 1, title: 'Finish Homework', completed: false, editing: false }]
    }
  },
  computed: {
    remaining () {
      return this.todos.filter(todo => !todo.completed).length
    },
    anyRemaining () {
      return this.remaining !== 0
    },
    todosFiltered () {
      if (this.filter === 'all') {
        return this.todos
      } else if (this.filter === 'active') {
        return this.todos.filter(todo => !todo.completed)
      } else if (this.filter === 'completed') {
        return this.todos.filter(todo => todo.completed)
      }
      return this.todos
    },
    showClearCompletedButton () {
      return this.todos.filter(todo => todo.completed).length > 0
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
      if (todo.title.trim().length === 0) {
        todo.title = this.beforeEditCache
      }
      todo.editing = false
    },
    cancelEditTodo (todo) {
      todo.title = this.beforeEditCache
      todo.editing = false
    },
    removeTodo (index) {
      this.todos.splice(index, 1)
    },
    /** TODO */
    checkAllTodos () {
      this.todos.forEach(todo => '')
    },
    clearCompleted () {
      this.todos = this.todos.filter(todo => !todo.completed)
    }
  }
}
</script>

<style>
    @import url("https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css");
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

    .todo-item-left {
      display: flex;
      align-items: center;
    }

    .todo-item-label {
      padding: 10px;
      border: 1px solid white;
    }

    .todo-item-edit {
      font-size: 24px;
      color: #2c3e50;
      margin-left: 12px;
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      font-family: Arial, Helvetica, sans-serif;
    }

    .todo-item-edit:focus {
      outline: none;
    }

    .completed {
      text-decoration: line-through;
      color: gray;
    }

    .remove-item {
      cursor: pointer;
      margin-left: 14px;
      font-size: 24px;
    }

    .remove-item:hover {
      color: red;
    }

    .extra-container {
      display: flex;
      align-items: center;
      justify-content: space-between;
      font-size: 16px;
      border-top: 1px solid lightgray;
      padding-top: 14px;
      margin-bottom: 14px;
    }

    button {
      font-size: 14px;
      background-color: white;
      appearance: none;
    }

    button.hover {
      background: lightgreen;
    }

    button.focus {
      outline: none;
    }

    .active {
      background: lightgreen;
    }

    /* CSS Transitions */
    .fade-enter-active, .fade-leave-active {
      transition: opacity .4s;
    }

    .fade-enter, .fade-leave-to {
      opacity: 0;
    }
</style>
