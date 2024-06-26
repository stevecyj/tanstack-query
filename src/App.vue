<script setup lang="ts">
import { ref, type Ref } from 'vue'
import { useQuery } from '@tanstack/vue-query'
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import { VueQueryDevtools } from '@tanstack/vue-query-devtools'

// const props = defineProps<{
//   id: number
// }>()
let todoId = ref<number>(1)

function fetchTodoById(id: number) {
  return fetch(`https://jsonplaceholder.typicode.com/todos/${id}`).then((response) =>
    response.json()
  )
}

function useTodo(id: Ref<number>) {
  return useQuery({
    queryKey: ['TODO', todoId],
    queryFn: () => fetchTodoById(id.value)
  })
}

// const { data, error, isFetching } = useTodo(todoId)

function handleClick() {
  console.log('click')
  todoId.value++
}

function handleChange() {
  console.log('change')
}
</script>

<template>
  <header>
    <VueQueryDevtools />
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
    <button @click="handleClick">click</button>
    <!-- <select v-model="todoId" @change="handleChange">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
      <option value="4">4</option>
    </select>
    <select v-model="todoId" @change="handleChange">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
      <option value="4">4</option>
    </select> -->
    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
