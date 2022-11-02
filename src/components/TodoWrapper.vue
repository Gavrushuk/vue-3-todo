<script lang="ts" setup>
import TodoCreateForm from '@/components/TodoCreateForm.vue';
import TodoList from '@/components/TodoList.vue';
import TodoListFooter from '@/components/TodoListFooter.vue';
import { computed, onMounted, ref, type Ref } from 'vue';
import TodoListFilters from './TodoListFilters.vue';
import { breakpointsBootstrapV5, useBreakpoints } from '@vueuse/core';

const breakpoints = useBreakpoints(breakpointsBootstrapV5);

const isDesktop = breakpoints.greater('md');

const todos: Ref<any[]> = ref([]);
const filters = ['All', 'Activate', 'Complete'];
const activeFilter = ref('All');

const filteredTodos = computed(() => {
  switch (activeFilter.value) {
    case 'Activate':
      return todos.value.filter((todo) => !todo.completed);

    case 'Complete':
      return todos.value.filter((todo) => todo.completed);
  
    default:
      return todos.value;
  }
});

const notCompletedTodosCount = computed(() => {
  return filteredTodos.value?.filter((todo) => !todo.completed).length || 0;
});

function createTodoItem(todo: any) {
  if (!todo) return;

  todos.value.push({
    title: todo,
    completed: false
  });

  updateTodosList();
}

function removeTodoItem(index: number) {
  todos.value.splice(index, 1);
  updateTodosList();
}

function toggleTodoItem(index: number) {
  let todoItem = todos.value[index];
  
  todoItem.completed = !todoItem.completed;
  updateTodosList();
}

function clearCompletedTodos() {
  todos.value = todos.value.filter((todo) => !todo.completed);
  updateTodosList();
}

function selectFilter(filter: string) {
  activeFilter.value = filter;
}

function syncTodosList() {
  try {
    if (localStorage.todosList) {
      todos.value = JSON.parse(localStorage.todosList);
    }
  } catch (error) {
    console.error(error);
    todos.value = [];
  }
}

function updateTodosList() {
  localStorage.setItem('todosList', JSON.stringify(todos.value));
  syncTodosList();
}

onMounted(() => {
  syncTodosList();
});
</script>

<template>
  <div class="todo-wrapper">
    <div class="container">
      <div class="todo-header">
        <div class="title">TODO</div>
        <div class="theme-switcher">
          <img class="light-theme-icon" src="@/assets/light-theme-icon.svg" alt="">
          <!-- <img class="light-theme-icon" src="@/assets/dark-theme-icon.svg" alt=""></img> -->
        </div>
      </div>

      <TodoCreateForm
        @create="createTodoItem"
      />

      <div class="todo-list-wrapper">
        <TodoListFooter
          :filters="filters"
          :activeFilter="activeFilter"
          :itemsLeftCount="notCompletedTodosCount"
          @clearCompleted="clearCompletedTodos"
          @selectFilter="selectFilter"
        />

        <TodoListFilters
          v-if="!isDesktop"
          :filters="filters"
          :activeFilter="activeFilter"
          @selectFilter="selectFilter"
        />

        <TodoList
          :list="filteredTodos"
          @toggle="toggleTodoItem"
          @remove="removeTodoItem"
        />
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.container {
  max-width: 590px;
  width: 100%;
  margin: 0 auto;
  padding: 24px;
}
.todo-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-top: 56px;
  .title {
    font-family: 'Josefin Sans';
    font-weight: 700;
    font-size: 36px;
    line-height: 36px;
    letter-spacing: 0.5em;
    color: #FFFFFF;
  }
  .theme-switcher {
    .light-theme-icon {
      width: 32px;
      height: 32px;
    }
  }
}
.todo-create-form {
  margin-top: 35px;
}
.todo-list-wrapper {
  display: flex;
  flex-direction: column;
  gap: 1px;
  background: #383A4F;
  border-radius: 6px;
  margin-top: 24px;
}
.todo-list-filters {
  background: #25273C;
  border-radius: 4px;
  padding: 14px;
  justify-content: center;
  gap: 16px;
  // margin-top: 24px;
}
@media (max-width: 768px) {
  .todo-header {
    padding-top: 26px;
    .title {
      font-size: 24px;
      line-height: 24px;
    }
  }
}
</style>
