<script lang="ts" setup>
import TodoListFilters from '@/components/TodoListFilters.vue';
import { breakpointsBootstrapV5, useBreakpoints } from '@vueuse/core';

const breakpoints = useBreakpoints(breakpointsBootstrapV5);

const isDesktop = breakpoints.greater('md');

defineProps<{
  itemsLeftCount: number,
  filters: string[],
  activeFilter: string
}>();

const emit =  defineEmits<{
  (e: 'selectFilter', filter: string): void
  (e: 'clearCompleted'): void
}>();
</script>

<template>
  <div class="todo-list-footer">
    <div class="items-left-count">{{ itemsLeftCount || 0 }} items left</div>
    <TodoListFilters
      v-if="isDesktop"
      :filters="filters"
      :activeFilter="activeFilter"
      @selectFilter="emit('selectFilter', $event)"
    />
    <div @click="emit('clearCompleted')" class="clear-completed-btn">Clear completed</div>
  </div>
</template>

<style lang="scss" scoped>
.todo-list-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px;
  gap: 5px;
  background: #25273C;
  border-radius: 4px;
  color: #6C6E83;
  font-family: 'Josefin Sans';
  font-weight: 700;
  font-size: 14px;
  line-height: 14px;
  .items-left-count,
  .clear-completed-btn {
    font-weight: 600;
    flex: 1;
  }
  .clear-completed-btn {
    text-align: end;
    cursor: pointer;
    transition: opacity 0.3s;
    &:hover {
      color: #ffffff;
    }
  }
  @media (max-width: 768px) {
    padding: 18px 20px;
    font-size: 12px;
    line-height: 12px;
  }
}
</style>
