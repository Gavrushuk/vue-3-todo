<script lang="ts" setup>
defineProps<{
  filters: string[],
  activeFilter: string
}>();

const emit =  defineEmits<{
  (e: 'selectFilter', filter: string): void
  (e: 'clearCompleted'): void
}>();
</script>

<template>
  <div class="todo-list-filters">
    <div
      v-for="filter of filters"
      :key="filter"
      class="todo-list-filters__item"
      :class="{
        active: filter === activeFilter
      }"
      @click="emit('selectFilter', filter)"
    >{{ filter }}</div>
  </div>
</template>

<style lang="scss" scoped>
.todo-list-filters {
  display: flex;
  align-items: center;
  gap: 6px;
  flex: 1;
  .todo-list-filters__item {
    cursor: pointer;
    transition: 0.3s;
    color: #6C6E83;
    font-family: 'Josefin Sans';
    font-weight: 700;
    font-size: 14px;
    line-height: 14px;
    &:hover {
      color: #ffffff;
    }
    &.active {
      color: #4777DB !important;
    }
  }
  @media (max-width: 768px) {
    .todo-list-filters__item {
      font-size: 12px;
      line-height: 12px;
    }
  }
}
</style>
