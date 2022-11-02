<script lang="ts" setup>
const emit = defineEmits<{
  (e: 'create', todo: any): void
}>();

function create(inputElement: any) {
  emit('create', inputElement.value.trim());
  inputElement.value = '';
}
</script>

<template>
  <div class="todo-create-form">
    <input
      class="todo-create-input"
      placeholder="Create a new todo..."
      type="text"
      @keyup.enter="create(($event.target as HTMLInputElement))"
      @blur="create(($event.target as HTMLInputElement))"
    >
  </div>
</template>

<style lang="scss" scoped>
.todo-create-form {
  display: flex;
  padding: 20px;
  margin-top: 35px;
  height: 64px;
  background: #25273C;
  border-radius: 6px;
  padding-left: 56px;
  .todo-create-input {
    width: 100%;
    font-family: 'Josefin Sans';
    font-style: normal;
    font-weight: 600;
    font-size: 18px;
    line-height: 18px;
    color: #FFFFFF;
    background: transparent;
    border: 0;
    &:hover,
    &:focus,
    &:active {
      outline: 0 !important;
      box-shadow: none !important;
    }
    &::placeholder {
      color: #6C6E83;
    }
  }
  @media (max-width: 768px) {
    height: 48px;
    padding: 18px;
    padding-left: 56px;
    .todo-create-input {
      font-size: 12px;
      line-height: 12px;
    }
  }
}
</style>
