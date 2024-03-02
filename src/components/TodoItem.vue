<script setup>
import { defineProps } from 'vue'
import { Icon } from '@iconify/vue'
const props = defineProps({
  todo: {
    type: Object,
    required: true,
    default: () => {
      return
    }
  },
  index: {
    type: Number,
    required: true
  }
})
defineEmits(['toggle-complete', 'todo-edit', 'todo-update', 'todo-delete'])
</script>
<template>
  <div class="todo-item">
    <input type="checkbox" :checked="todo.isCompleted" @input="$emit('toggle-complete', index)" />
    <div>
      <input
        type="text"
        :value="todo.todo"
        v-if="todo.isEditing"
        @input="$emit('todo-update', $event.target.value, index)"
      />
      <p :class="{ 'todo-completed': todo.isCompleted }" v-else>
        {{ todo.todo }}
      </p>
    </div>
    <div class="todo-actions">
      <Icon
        v-if="todo.isEditing"
        icon="ph:check-circle"
        width="22"
        height="22"
        style="color: #41b080"
        @click="$emit('todo-edit', index)"
      />
      <Icon
        v-else
        icon="ph:pencil-fill"
        width="22"
        height="22"
        style="color: #41b080"
        @click="$emit('todo-edit', index)"
      />
      <Icon
        icon="ph:trash"
        width="22"
        height="22"
        style="color: #f00"
        @click="$emit('todo-delete', todo.id)"
      />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.todo-item {
  display: flex;
  align-items: center;
  padding: 10px;
  //   justify-content: space-between;
  gap: 20px;
  max-width: 600px;
  margin: 0 auto 10px;
  transition: all 0.3s ease-in-out;
  background: #e2e2e2;
  .todo-actions {
    opacity: 0;
    transition: all 0.3s ease-in-out;
    display: flex;
    align-items: center;
    gap: 10px;
    align-self: flex-end;
    svg {
      cursor: pointer;
    }
  }
  &:hover {
    background: #ddd;

    .todo-actions {
      opacity: 1;
    }
  }
  .todo-completed {
    text-decoration: line-through;
  }
}
</style>
