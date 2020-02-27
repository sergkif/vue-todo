<template>
  <div class="home">
    <Note :note="note" v-on:delete-todo="deleteTodo"/>
  </div>
</template>

<style lang="scss" scoped>
  .home {
    display: flex;
    justify-content: center;
    padding: 0;
    margin: 0;
  }
</style>

<script>
export default {
  name: 'Home',
  components: {
    Note: () => import('@/components/Note.vue')
  },
  data () {
    return {
      note: {
        id: 1,
        title: 'Note test',
        todos: [
          {
            id: 1,
            title: 'Go workout',
            completed: false
          },
          {
            id: 2,
            title: 'Do laundry',
            completed: false
          },
          {
            id: 3,
            title: 'Cook food',
            completed: false
          },
          {
            id: 4,
            title: 'Clean up room',
            completed: false
          },
          {
            id: 5,
            title: 'Finish work',
            completed: false
          }
        ]
      }
    }
  },
  methods: {
    deleteTodo(todoId) {
      this.note.todos = this.note.todos.filter(todo => todo.id !== todoId)
    }
  }
}
</script>
