<script setup>
import { ref, defineEmits, reactive } from 'vue'

import TodoButton from './TodoButton.vue';
const todoState = reactive({
  todo: '',
  invalid: null,
  errMsg: ""
})

const emit = defineEmits(['create-todo'])

function createTodo() {
  todoState.invalid = null
  if (todoState.todo !== '') {
    emit('create-todo', todoState.todo)
    todoState.todo = ''
    return;
  }
  todoState.invalid = true
  todoState.errMsg = "Todo can't be empty"
}
</script>
<template>
  <div class="todo-wrapper">
    <h1>Create Todo</h1>
    <div class="todo-form" :class="{'todo-error': todoState.invalid}">
      <input type="text" v-model="todoState.todo" />
      <TodoButton @click="createTodo">Create</TodoButton>
    </div>
    <p v-show="todoState.invalid" :class="{'todo-error-txt': todoState.invalid}">{{ todoState.errMsg }}</p>
  </div>
</template>

<style lang="scss" scoped>
.todo-wrapper {
  padding: 20px;
  max-width: 600px;
  margin: auto;
  text-align: center;
  h1 {
    font-size: 40px;
    line-height: 1.5;
    margin-bottom: 10px;
    font-weight: 600;
  }
  .todo-form {
    display: flex;
    border: 1px green solid;
    input {
      width: 90%;
      border: 0;
      outline: 0;
      padding: 10px;
    }
    button {
      width: 10%;
      border: 0;
      outline: 0;
    }
    &.todo-error {
      border-color: red;
    }
  }
  .todo-error-txt {
    color: red;
  }
}
</style>
