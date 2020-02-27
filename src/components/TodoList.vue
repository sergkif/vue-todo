<template>
  <div>
    <ul class="todoList">
      <li class="todoList_item" v-bind:key="todo.id" v-for="todo in todos">
        <Todo v-bind:todo="todo" v-on:delete-todo="$emit('delete-todo', todo.id)"/>
      </li>
    </ul>
  </div>
</template>

<style lang="scss" scoped>
  .todoList {
    list-style: none;
    color: #555;
    font-size: 22px;
    font-family: courier, monospace;
    padding: 0;
    margin: 0;

    &_item {
      list-style: none;
      border-bottom: 1px dotted #ccc;
      text-indent: 25px;
      height: auto;
      text-transform: capitalize;

      :hover {
        background-color: #f0f0f0;
        transition: all 0.2s;
      }
    }
  }
</style>

<script>
export default {
  name: "TodoList",
  components: {
    Todo: () => import('@/components/Todo.vue')
  },
  props: [
    "todos"
  ]  
}
</script>
