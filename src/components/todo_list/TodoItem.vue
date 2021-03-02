<template>
    <div class="todo-item">
        <div class="todo-item-left">
           <input type="checkbox" v-model="completed">
           <div v-if="!todo.editing" class="todo-item-label" :class="{completed : completed}"
              @dblclick="editTodo">{{ title }}</div>
           <input v-else type="text" class="todo-item-edit" v-model="title"
              @blur="doneEditTodo" @keyup.enter="doneEditTodo" @keyup.esc="cancelEditTodo" v-focus>
        </div>
        <div class="remove-item" @click="removeTodo(index)">
            &times;
        </div>
    </div>
</template>

<script>
export default {
  name: 'todo-item',
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  data () {
    return {
      id: this.todo.id,
      title: this.todo.title,
      completed: this.todo.completed,
      editing: this.todo.editing,
      beforeEditCache: ''
    }
  },
  methods: {
    removeTodo (index) {
      this.$emit('removeTodo', index)
    },
    editTodo () {
      this.beforeEditCache = this.title
      this.editing = true
    },
    doneEditTodo () {
      if (this.title.trim().length === 0) {
        this.title = this.beforeEditCache
      }
      this.editing = false
    },
    cancelEditTodo () {
      this.title = this.beforeEditCache
      this.editing = false
    }
  }
}
</script>
