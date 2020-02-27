<template>
  <div class="todo" >
    <span class="todo_title" v-bind:class="{ 'todo_title__completed': todo.completed }" @click="markComplete">{{ todo.title }}</span>
    <div class="todo_checkbox" @click="markComplete"><input class="todo_checkbox_input" type="checkbox" v-model="todo.completed"></div>
    <button class="todo_button" @click="$emit('delete-todo', todo.id)">Delete</button>
  </div>
</template>

<style lang="scss" scoped>
  .todo {
    display: grid;
    grid-template-areas: "title checkbox button";
    grid-template-columns: 8fr 1fr 1fr;

    &_title {
      grid-area: title;
      text-align: start;
      cursor: pointer;
      padding: 10px;
      
      &__completed {
        text-decoration: line-through;
      }
    }

    &_checkbox {
      grid-area: checkbox;
      cursor: pointer;
      padding: 10px;

      &_input {
        cursor: pointer;
      }
    }

    &_button {
      grid-area: button;
      padding: 10px;
    }
  }
</style>

<script>
export default {
  name: 'Todo',
  props: [
    "todo"
  ],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed
    }
  }
}
</script>