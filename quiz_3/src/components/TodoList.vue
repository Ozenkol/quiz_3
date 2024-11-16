<script setup lang="ts">
  import { ref, computed } from 'vue';
  import TodoItem from './TodoItem.vue';
  let currId = 0
  interface TodoItem {
    id: number, 
    title: string,
    priority: string, 
    completed: boolean
  }
  const todoList = ref<TodoItem[]>([ 
  ])
  const newItem = ref<TodoItem>(
    {
      id: currId++,
      title: '',
      priority: '', 
      completed: false
    }
  )
  const title = computed({
    get() {
      return newItem.value?.title || ''
    },
    set(title) {
      if (typeof newItem.value?.title === 'string') {
        newItem.value = { ...newItem.value, title }
      }
    },
  })
  const priority = computed({
    get() {
      return newItem.value?.priority || ''
    },
    set(priority) {
      if (typeof newItem.value?.priority === 'string') {
        newItem.value = { ...newItem.value, priority }
      }
    },
  })
  function addItem() {
    todoList.value.push(newItem.value)
  }
  // function delete(todo_id:number): void {
  //   var index = todoList.value.map(x => {
  //     return x.id;
  //   }).indexOf(todo_id);
  //   todoList.value.splice(index, 1);
  // }
</script>

<template>
  <input type="text" v-model="title"> <button @click="addItem()">Add task</button>
  <select class="form-control" v-model="priority">
    <option v-bind:value="'high'" >High</option>
    <option v-bind:value="'medium'" >Medium</option>
    <option v-bind:value="'medium'" >Low</option>
  </select>
  
  <TransitionGroup name="list" tag="ul">
    <li v-for="item in todoList" :key="item.id">
      <TodoItem :item="item">
        <button @click="">Delete</button>
      </TodoItem>
    </li>
  </TransitionGroup>
</template>

<style scoped>
  input {
    width: 5em;
    height: 2em;
  }
  button {
    height: 2em;
  }
  .list-enter-active,
  .list-leave-active {
    transition: all 0.5s ease;
  }
  .list-enter-from,
  .list-leave-to {
    opacity: 0;
    transform: translateX(30px);
  }
</style>
