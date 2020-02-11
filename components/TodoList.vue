<template>
  <div class="todo-list">
    <ul>
      <TodoListItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        :on-delete="deleteTodo"
        :on-update="updateTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoListItem from './TodoListItem'

export default {
  name: 'TodoList',
  components: {
    TodoListItem
  },
  props: {
    msg: {
      type: String,
      default: ''
    },
    todos: {
      type: Array,
      default: () => []
    },
    onUpdateTodos: {
      type: Function,
      default: () => ({})
    }
  },
  methods: {
    deleteTodo(id) {
      const todos = this.todos.filter((todo) => todo.id !== id)
      this.onUpdateTodos(todos)
    },
    updateTodo(updatedTodo) {
      const todos = this.todos.map((todo) =>
        todo.id === updatedTodo.id ? updatedTodo : todo
      )
      this.onUpdateTodos(todos)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
ul {
  list-style-type: none;
  padding: 0;
  border: thin solid rgba(0, 0, 0, 0.2);
  width: 400px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;

  &:empty {
    display: none;
  }
}
a {
  color: #42b983;
}
</style>
