<template>
  <input
    v-model="newTodo"
    autofocus
    placeholder="Enter a new Todo"
    @keyup.enter="addTodo"
  />
</template>

<script>
import generateId from '~/utils/generateId'

export default {
  name: 'NewToDoItem',
  props: {
    onAddTodo: {
      type: Function,
      default: () => {}
    }
  },
  data() {
    return {
      newTodo: ''
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo) {
        this.onAddTodo({
          id: generateId(),
          note: this.newTodo,
          complete: false
        })
        this.newTodo = ''
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
input {
  width: 400px;
  font-size: 14px;
  padding: 10px;
  border: thin solid #cccccc;
  margin-bottom: -1px;
  outline: 0;
  position: relative;

  &:focus {
    z-index: 999;
    box-shadow: 0px 0px 0 2px #2196f3;
  }
}
</style>
