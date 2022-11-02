<script lang="ts" setup>
const props = defineProps<{
  item: any,
  index: number
}>();

const emit = defineEmits<{
  (e: 'toggle', index: number): void,
  (e: 'remove', index: number): void
}>();
</script>

<template>
  <div
    class="todo-item"
    :class="{
      completed: item.completed
    }"
  >
    <label
      class="todo-item__checkbox"
      :for="`checkbox${index}`"
    >
      <input
        type="checkbox"
        :checked="item.completed"
        :id="`checkbox${index}`"
        @input="emit('toggle', index)"
      />
      <span class="checkmark"></span>
    </label>

    <div class="todo-item__title">{{ item.title }}</div>

    <div @click.prevent="emit('remove', index)" class="todo-item__remove">
      <img src="@/assets/remove-todo-item-icon.svg" class="todo-item__remove__icon" alt="">
    </div>
  </div>
</template>

<style lang="scss" scoped>
.todo-item {
  display: flex;
  gap: 16px;
  background: #25273C;
  border-radius: 4px;
  padding: 20px;
  cursor: pointer;
  &:hover {
    .todo-item__remove {
      opacity: 1;
    }
    .todo-item__checkbox .checkmark {
      background-color: rgba($color: #ffffff, $alpha: 0.1);
    }
    .todo-item__checkbox .todo-item__title {
      color: rgba($color: #ffffff, $alpha: 0.8);
    }
  }
  &.completed {
    .checkmark {
      background: linear-gradient(142.13deg, #6EBAF8 6.56%, #AD7AF9 87.81%);
    }
    .todo-item__title {
      text-decoration: line-through;
      color: #6C6E83;
    }
  }
  .todo-item__title {
    font-family: 'Josefin Sans';
    font-style: normal;
    font-weight: 600;
    font-size: 18px;
    line-height: 18px;
    color: #FFFFFF;
    margin-top: 3px;
    transition: opacity 0.3s;
    width: 100%;
  }
  .todo-item__checkbox {
    display: block;
    position: relative;
    padding-left: 20px;
    cursor: pointer;
    font-size: 22px;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }
  .todo-item__checkbox input {
    position: absolute;
    opacity: 0;
    cursor: pointer;
    height: 0;
    width: 0;
  }
  .checkmark {
    position: absolute;
    top: 0;
    left: 0;
    height: 20px;
    width: 20px;
    border: 1px solid #303247;
    border-radius: 50%;
    transition: 0.3s;
  }
  .checkmark:after {
    content: "";
    position: absolute;
    display: none;
  }
  .todo-item__checkbox input:checked ~ .checkmark:after {
    display: block;
  }
  .todo-item__checkbox .checkmark:after {
    left: 10px;
    top: 9px;
    width: 5px;
    height: 10px;
    border: solid white;
    border-width: 0 3px 3px 0;
    transform: translate(-50%, -50%) rotate(45deg);
  }
  .todo-item__remove {
    width: 20px;
    height: 20px;
    min-width: 20px;
    cursor: pointer;
    opacity: 0;
    transition: opacity 0.3s;
    user-select: none;
    .todo-item__remove__icon {
      width: 100%;
      height: 100%;
    }
  }
  @media (max-width: 768px) {
    padding: 16px 20px;
    .todo-item__title {
      font-size: 12px;
      line-height: 12px;
      margin-top: 5px;
    }
    .todo-item__remove {
      opacity: 1;
    }
  }
}
</style>
