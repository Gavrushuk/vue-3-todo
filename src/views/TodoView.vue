<script setup lang="ts">
import TodoWrapper from '@/components/TodoWrapper.vue';
</script>

<template>
  <div class="todo-view">
    <div class="todo-main-bg"></div>
    <TodoWrapper />
  </div>
</template>

<style lang="scss" scoped>
.todo-view {
  position: relative;
  background: #161622;
  min-height: 100vh;
  width: 100%;
  .todo-main-bg {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    width: 100%;
    height: 300px;
    background-image: url("@/assets/todo-main-bg.png");
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    @media (max-width: 768px) {
      height: 200px;
    }
  }
  .todo-wrapper {
    position: relative;
  }
}
</style>
