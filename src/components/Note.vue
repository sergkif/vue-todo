<template>
  <div class="note">
    <div class="note_title">
      <h2>{{ note.title }}</h2>
    </div>
    <div class="note_todos">
      <TodoList :todos="note.todos" v-on:delete-todo="deleteTodo"/>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .note {
    display: grid;
    grid-template-areas: "title" "todos";
    border: 1px solid #dedede;
    width: 40%;
    padding: 0;
    margin: 0;

    &_title {
      grid-area: title;
      border-bottom: 1px solid #dedede;
    }

    &_todos {
      grid-area: todos;
    }
  }
</style>

<script>
export default {
  name: "Note",
  components: {
    TodoList: () => import('@/components/TodoList.vue')
  },
  props: {
    note: {
      type: Object,
      required: true
    }
  },
  methods: {
    deleteTodo (todoId) {
      this.$emit('delete-todo', todoId)
    }
  }
}
</script>
