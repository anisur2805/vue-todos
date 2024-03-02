<script setup>
import { computed, ref, watch } from 'vue'
import { uid } from 'uid'
import TodoCreator from '@/components/TodoCreator.vue'
import { Icon } from '@iconify/vue'
import TodoItem from '@/components/TodoItem.vue'

const todoList = ref([])

watch(
  todoList,
  () => {
    setTodoListLocalStorage()
  },
  {
    deep: true
  }
)

const setTodoListLocalStorage = () => {
  localStorage.setItem('todoList', JSON.stringify(todoList.value))
}

const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem('todoList'))
  if (savedTodoList) {
    todoList.value = savedTodoList
  }
}

fetchTodoList()

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null
  })
}

const toggleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted
}

const todoEdit = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing
}

const todoUpdate = (newValue, todoPos) => {
  todoList.value[todoPos].todo = newValue
}

const todoDelete = (todoId) => {
  todoList.value = todoList.value.filter((t) => t.id !== todoId)
}

const todoCompleted = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted)
})

</script>
<template>
  <div class="todo-wrapper">
    <TodoCreator @create-todo="createTodo" />
    <ul v-if="todoList.length > 0">
      <TodoItem
        v-for="(todo, index) in todoList"
        :todo="todo"
        :index="index"
        :key="todo.id"
        @toggle-complete="toggleTodoComplete"
        @todo-edit="todoEdit"
        @todo-update="todoUpdate"
        @todo-delete="todoDelete"
      />
    </ul>
    <p v-else class="todo-msg">
      <Icon icon="iconoir:emoji" width="22" height="22" style="color: #41b080" />
      You have not create any Todos yet.
    </p>
    <p class="all-todo-completed"  v-if="todoCompleted && todoList.length > 0">You have completed all todos!</p>
  </div>
</template>

<style scoped>
.todo-msg {
  justify-content: center;
  display: flex;
  align-content: center;
  gap: 5px;
}

.all-todo-completed {
  text-align: center;
  color: green;
  margin: 10px;
}
</style>
