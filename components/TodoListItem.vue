<template>
  <li class="todo-item" :class="{ 'is-complete': isComplete }">
    <input
      v-model="isComplete"
      class="completed"
      type="checkbox"
      @change="toggleTodo"
    />
    <input v-model="note" class="note" type="text" @blur="updateTodo" />
    <button class="delete" @click="removeTodo">❌</button>
  </li>
</template>

<script>
export default {
  name: 'TodoListItem',
  props: {
    todo: {
      type: Object,
      default: () => ({})
    },
    onDelete: {
      type: Function,
      default: () => ({})
    },
    onUpdate: {
      type: Function,
      default: () => ({})
    }
  },
  data() {
    return {
      isComplete: this.todo.complete,
      note: this.todo.note
    }
  },
  methods: {
    removeTodo() {
      this.onDelete(this.todo.id)
    },
    toggleTodo() {
      this.onUpdate({ ...this.todo, complete: !this.todo.complete })
    },
    updateTodo() {
      this.onUpdate({ ...this.todo, note: this.note })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
li {
  display: flex;
  width: 100%;
  text-align: left;
  border-bottom: thin solid #cccccc;
  position: relative;
  align-items: center;
}

.completed {
  font-size: 16px;
  margin: 0 10px;
}

.note {
  flex: 1;
  border: 0;
  margin: 0;
  padding: 10px;
  font-size: 14px;
  outline: 0;
  &:focus {
    z-index: 999;
    box-shadow: 0px 0px 0 2px #2196f3;
  }
}

.delete {
  right: 0;
  padding: 9px 8px 9px 12px;
  border: none;
  outline: 0;
  &:focus {
    z-index: 999;
    box-shadow: 0px 0px 0 2px #2196f3;
  }
}
</style>
