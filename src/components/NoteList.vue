<template>
  <div class="noteList">
    <section class="noteList_section" v-for="note in notes" :key="note.id" @click="openModal(note.id)">
      <Note :note="note" :modalId="modalId" 
      v-on:delete-todo="deleteTodo" v-on:mark-complete="markComplete" v-on:save-new-title="saveNewTitle" v-on:delete-note="deleteNote"/>
    </section>
    <div v-if="error" class="noteList_error">{{ error }}</div>
  </div>
</template>

<style lang="scss" scoped>
  .noteList {
    width: 40%;

    &_section {
      padding: 5px;
    }

    &_error {
      color: #D8000C;
    }
  }
</style>

<script>
export default {
  name: "NoteList",
  components: {
    Note: () => import('@/components/Note.vue')
  },
  data () {
    return {
      notes: {},
      error: '',
      modalId: null
    }
  },
  methods: {
    openModal (noteId) {
      this.modalId = noteId
    },
    deleteTodo (todoId, noteId) {
      this.notes.forEach(note => {
        if (note.id === noteId) {
          note.todos = note.todos.filter(todo => todo.id !== todoId)
          this.deleteTodoFetch(noteId)
        }
      })
    },
    async onInit () {
      await fetch('http://localhost:3000/notes', {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json'
        }
      })
        .then(response => {
          if (response.status === 200) {
            return response.json()
          } else {
            throw new Error(response.statusText)
          }
        })
        .then(data => {
          if (data) this.notes = data
        })
        .catch(err => {
          console.log(err)
          this.error = err
        })
    },
    async deleteTodoFetch (noteId) {
      await fetch('http://localhost:3000/notes/' + noteId, {
        method: 'PUT',
        headers: {
          Accept: 'application/json',
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.notes.find(note => note.id === noteId))
      })
        .then(response => {
          if (response.status !== 200) {
            throw new Error(response.statusText)
          }
        })
        .catch(err => console.log(err))
    },
    async saveEditNote (noteId) {
      await fetch('http://localhost:3000/notes/' + noteId, {
        method: 'PUT',
        headers: {
          Accept: 'application/json',
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.notes.find(note => note.id === noteId))
      })
        .then(response => {
          if (response.status !== 200) {
            throw new Error(response.statusText)
          }
        })
        .catch(err => console.log(err))
    },
    saveNewTitle (newTitle, noteId) {
      this.notes.forEach(note => {
        if (note.id === noteId) {
          note.title = newTitle
          this.saveEditNote(noteId)
        }
      })
    },
    markComplete (noteId) {
      this.saveEditNote(noteId)
    },
    deleteNote (noteId) {
      this.notes = this.notes.filter(note => note.id !== noteId)
      this.deleteNoteFetch(noteId)
    },
    async deleteNoteFetch (noteId) {
      await fetch('http://localhost:3000/notes/' + noteId, {
        method: 'DELETE',
      })
        .then(response => {
          if (response.status !== 200) {
            throw new Error(response.statusText)
          }
        })
        .catch(err => console.log(err))
    }
  },
  mounted () {
    this.onInit()
  }
}
</script>
