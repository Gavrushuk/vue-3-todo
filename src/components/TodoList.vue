<script lang="ts" setup>
import TodoListItem from './TodoListItem.vue';

const props = defineProps<{
  list: any[]
}>();

const emit = defineEmits<{
  (e: 'toggle', index: number): void,
  (e: 'remove', index: number): void
}>();
</script>

<template>
  <div class="todo-list">
    <TodoListItem
      v-for="(item, index) of list"
      :key="index"
      :item="item"
      :index="index"
      @toggle="emit('toggle', $event)"
      @remove="emit('remove', $event)"
    />

    <div v-if="!list.length" class="todo-list-default">List is empty</div>
  </div>
</template>

<style lang="scss" scoped>
.todo-list {
  display: flex;
  flex-direction: column;
  gap: 1px;
  .todo-list-default {
    font-family: 'Josefin Sans';
    font-weight: 600;
    font-size: 14px;
    line-height: 14px;
    text-align: center;
    padding: 20px;
    background: #25273C;
    color: #6C6E83;
  }
}
</style>
