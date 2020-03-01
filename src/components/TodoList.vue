<template>
  <div>
    <ul class="todoList">
      <li class="todoList_item" :class="{ todoList_item__activeHover: isModal }" v-bind:key="todo.id" v-for="todo in todos">
        <Todo :todo="todo" :isModal="isModal" v-on:delete-todo="$emit('delete-todo', todo.id)" v-on:mark-complete="$emit('mark-complete')"/>
      </li>
    </ul>
  </div>
</template>

<style lang="scss" scoped>
  .todoList {
    user-select: none;
    list-style: none;
    color: #555;
    padding: 0;
    margin: 0;

    &_item {
      list-style: none;
      border-bottom: 1px dotted #ccc;
      text-indent: 25px;
      height: auto;
      text-transform: capitalize;

      &__activeHover {
        :hover {
          background-color: #f0f0f0;
          transition: all 0.2s;
        }
      }
    }

    :last-child {
      border: none;
    }
  }
</style>

<script>
export default {
  name: "TodoList",
  components: {
    Todo: () => import('@/components/Todo.vue')
  },
  props: {
    todos: {
      type: Array,
      required: false,
      default: () => {}
    },
    isModal: {
      type: Boolean,
      required: false,
      default: false
    }
  }
}
</script>
