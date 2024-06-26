<script setup lang="ts">
import { ref, type Ref } from 'vue'
import { useQuery } from '@tanstack/vue-query'

let todoId = ref<number>(1)

function fetchTodoById(id: number) {
  return fetch(`https://jsonplaceholder.typicode.com/todos/${id}`).then((response) =>
    response.json()
  )
}

function useTodo(id: Ref<number>) {
  return useQuery({
    queryKey: ['TODO', todoId],
    queryFn: () => fetchTodoById(id.value),
    staleTime: 5 * 1000
  })
}

const { data, error, isFetching, isLoading } = useTodo(todoId)

function handleChange() {
  console.log('change')
}
</script>

<template>
  <header>
    <select v-model="todoId" @change="handleChange">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
      <option value="4">4</option>
    </select>
  </header>
  <div v-if="isLoading || isFetching">Loading</div>
  <div>
    <pre>{{ data }}</pre>
  </div>
</template>

<style scoped></style>
