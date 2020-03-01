<template>
  <div class="todo" >
    <span class="todo_title" :class="{ 'todo_title__completed': todo.completed }" @click="markComplete">{{ todo.title }}</span>
    <div class="todo_checkbox" @click="markComplete">
      <input class="todo_checkbox_input" :disabled="!isModal" type="checkbox" v-model="todo.completed">
    </div>
    <div class="todo_button" :class="{ todo_button__activeHover: isModal }" @click="deleteTodo(todo.id)">
      <img class="todo_button_image" src="">
    </div>
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
      display: flex;

      &_image {
        content: url("../assets/delete-24px.svg");
        padding: 10px;
        width: stretch;
      }

      &__activeHover {
        :hover {
          transition: .5s;
          background-color: #9c9c9c;
        }
      }
    }

    &_delete {
      display: block;
      text-indent: -9999px;
      width: 100px;
      height: 82px;
      background: url(/assets/delete-24px.svg);
      background-size: 24px 24px;
    }
  }
</style>

<script>
export default {
  name: 'Todo',
  props: {
    todo: {
      type: Object,
      required: true
    },
    isModal: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  methods: {
    markComplete() {
      if (this.isModal) {
        this.todo.completed = !this.todo.completed
        this.$emit('mark-complete')
      }
    },
    deleteTodo(todoId) {
      if (this.isModal) this.$emit('delete-todo', todoId)
    }
  }
}
</script>