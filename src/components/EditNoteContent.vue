<template>
  <div class="editNoteContent">
    <section class="editNoteContent_title">
      <EditInput noteKey="Title" :noteValueProps="note.title" :id="getId" v-on:data-changed="changeTitle"/>
    </section>
    <section class="editNoteContent_todos">
      <section class="editNoteContent_todos_todo" v-for="todo in note.todos" :key="todo.id">
        <EditInput noteKey="Todo" :noteValueProps="todo.title" :id="getId" v-on:data-changed="changeTodo"/>
      </section>
    </section>
  </div>
</template>

<style lang="scss" scoped>
  .editNoteContent {
    display: grid;

    &_title {
      padding: 5px;
    }

    &_todos {
      &_todo {
        padding: 5px;
      }
    }
  }
</style>

<script>
export default {
  name: "EditNoteContent",
  components: {
    EditInput: () => import('@/components/EditInput.vue')
  },
  props: {
    note: {
      type: Object,
      required: false,
      default: () => ({
        id: null,
        title: '',
        todos: []
      })
    }
  },
  computed: {
    getId() {
      if (this.note.id) return this.note.id.toString()
      else return ''
    }
  },
  methods: {
    changeTitle (newTitle) {
      this.$emit('title-changed', newTitle)
    },
    changeTodo (newTitle, todoId) {
      this.$emit('todo-changed', newTitle, todoId)
    }
  }
}
</script>
