<template>
  <div class="note">
    <div class="note_title" :class="{ note_title__cutted: note.id !== modalId }">
      <NoteHeader :title="note.title" :isModal="note.id == modalId" v-on:edit-note="editNote" v-on:delete-note="$emit('delete-note', note.id)"/>
    </div>
    <div class="note_todos" :class="{ note_todos__cutted: note.id !== modalId }">
      <TodoList :isModal="note.id == modalId" :todos="note.todos" v-on:delete-todo="deleteTodo" v-on:mark-complete="markComplete"/>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .note {
    display: grid;
    grid-template-areas: "title" "todos";
    border: 1px solid #dedede;
    padding: 0;
    margin: 0;
    font-size: 22px;
    font-family: courier, monospace;

    &_title {
      grid-area: title;
      border-bottom: 1px solid #dedede;

      &__cutted {
        display: block;
        height: 40px;
        font-size: 12px;
        overflow: hidden;
        cursor: pointer;
      }
    }

    &_todos {
      grid-area: todos;

      &__cutted {
        height: 90px;
        overflow: hidden;
        cursor: pointer;

        > :after{
          content: "";
          display: block;
          height: 40px;
          position: relative;
          top: -87px;
          background-image: linear-gradient(to bottom, rgba(255, 255, 255, 0), #fff 75%)
        }
      }
    }
  }
</style>

<script>
export default {
  name: "Note",
  components: {
    TodoList: () => import('@/components/TodoList.vue'),
    NoteHeader: () => import('@/components/NoteHeader.vue')
  },
  props: {
    note: {
      type: Object,
      required: true
    },
    modalId: {
      type: Number,
      required: false,
      default: null
    }
  },
  methods: {
    deleteTodo (todoId) {
      this.$emit('delete-todo', todoId, this.note.id)
    },
    markComplete () {
      this.$emit('mark-complete', this.note.id)
    },
    saveNewTitle (newTitle) {
      this.$emit('save-new-title', newTitle, this.note.id)
    },
    editNote () {
      this.$router.push({ name: 'EditPage', params: { id: this.note.id, note: this.note } })
    },
  }
}
</script>
