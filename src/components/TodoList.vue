<template>
  <div>
    <BaseInputText
      v-model="newTodoText"
      placeholder="New todo"
      @keydown.enter="addTodo"
    />
    <ol v-if="todos.length">
      <TodoListItem
        v-for="todo in sorted_todos"
        :key="todo.id"
        :todo="todo"
        @remove="removeTodo"
      />
    </ol>
    <p v-else>
      Nothing left in the list. Add a new todo in the input above.
    </p>
  </div>
</template>

<script>
  import BaseInputText from './BaseInputText.vue'
  import TodoListItem from './TodoListItem.vue'

  let nextTodoId = 1

  export default {
    components: {
      BaseInputText, TodoListItem
    },
    data() {
      return {
        newTodoText: '',
        todos: [
          {
            id: nextTodoId++,
            text: 'Fall in love'
          },
          {
            id: nextTodoId++,
            text: 'Learn about single-file components'
          },
          {
            id: nextTodoId++,
            text: 'Learn Vue'
          }
        ]
      }
    },
    methods: {
      addTodo() {
        const trimmedText = this.newTodoText.trim()
        if (trimmedText) {
          this.todos.push({
            id: nextTodoId++,
            text: trimmedText
          })
          this.newTodoText = ''
        }
      },
      removeTodo(idToRemove) {
        this.todos = this.todos.filter(todo => {
          return todo.id !== idToRemove
        })
      }
    },
    computed: {
      sorted_todos() {
        return this.todos.sort(function (a, b) {
          return b.id - a.id
        })
      }
    }
  }
</script>
