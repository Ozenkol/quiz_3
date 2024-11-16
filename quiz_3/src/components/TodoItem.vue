<script setup lang="ts">
import { ref } from 'vue';

  interface TodoItem {
    id: number, 
    title: string,
    priority: string, 
    completed: boolean
  }

  const props = defineProps<{
    item: TodoItem
  }>()
    const emit = defineEmits<{
      (e: 'delete', value: string): void
    }>()
  
</script>

<template>
  <Transition>
    <div class="item">
      <div class="item__content" :class="{'completed': item.completed }">
        {{ item.title }}
      </div>
    </div>
  </Transition>
</template>

<style scoped>
  .v-enter-active,
  .v-leave-active {
    transition: opacity 0.5s ease;
  }

  .v-enter-from,
  .v-leave-to {
    opacity: 0;
  }
  .item {
    border: solid;
  }
  .completed {
    text-decoration: overline;
  }
</style>
