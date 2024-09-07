<template>
  <div class="container mx-auto p-4">
    <h1 class="text-3xl font-bold mb-4">Todo List</h1>
    <div class="mb-4">
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        type="text"
        placeholder="새로운 할 일을 입력하세요"
        class="w-full p-2 border rounded"
      />
    </div>
    <ul>
      <li
        v-for="todo in todos"
        :key="todo.id"
        class="flex items-center justify-between p-2 border-b"
      >
        <div class="flex items-center flex-grow mr-4">
          <input
            type="checkbox"
            v-model="todo.completed"
            class="mr-2"
          />
          <input
            v-if="todo.isEditing"
            v-model="todo.text"
            @blur="finishEdit(todo)"
            @keyup.enter="finishEdit(todo)"
            type="text"
            class="flex-grow p-1 border rounded"
          />
          <span
            v-else
            @dblclick="startEdit(todo)"
            :class="{ 'line-through': todo.completed }"
          >
            {{ todo.text }}
          </span>
        </div>
        <div>
          <button @click="removeTodo(todo.id)" class="text-red-500 mr-2">삭제</button>
          <button @click="startEdit(todo)" class="text-blue-500" v-if="!todo.isEditing">수정</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

interface Todo {
  id: number
  text: string
  completed: boolean
  isEditing: boolean
}

const newTodo = ref('')
const todos = ref<Todo[]>([])

const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      id: Date.now(),
      text: newTodo.value,
      completed: false,
      isEditing: false
    })
    newTodo.value = ''
  }
}

const removeTodo = (id: number) => {
  todos.value = todos.value.filter(todo => todo.id !== id)
}

const startEdit = (todo: Todo) => {
  todo.isEditing = true
}

const finishEdit = (todo: Todo) => {
  todo.isEditing = false
  todo.text = todo.text.trim()
  if (!todo.text) {
    removeTodo(todo.id)
  }
}
</script>

<style>
@import 'tailwindcss/base';
@import 'tailwindcss/components';
@import 'tailwindcss/utilities';
</style>