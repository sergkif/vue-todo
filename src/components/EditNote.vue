<template>
  <div class="editNote">
    <div class="editNote_title">
      <h1><span v-if="note.id">Edit</span><span v-else>Add</span> note<span v-if="note.id">: "{{ note.title }}"</span></h1>
    </div>
    <div class="editNote_content">
      <EditNoteContent :note="note" v-on:title-changed="changeTitle" v-on:todo-changed="changeTodo"/>
    </div>
    <div class="editNote_add" @click="addTodo">
      <img class="editNote_add_image"> Add Todo
    </div>
    <div class="editNote_save">
      <ButtonEditNote buttonLabel="Cancel" color="#8f0404" @click="$router.push({ path: '/' })"/>
      <ButtonEditNote buttonLabel="Save" color="#0e4000" @click="saveNote"/>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .editNote {
    display: grid;
    grid-template-areas: "title" "content" "add" "save";
    padding: 0;
    margin: 0;
    font-family: courier, monospace;
    width: 40%;
    grid-gap: 10%;

    &_title {
      grid-area: title;
    }

    &_content {
      grid-area: content;
    }

    &_add {
      grid-area: add;
      display: flex;
      align-items: center;
      cursor: pointer;
      width: fit-content;
      padding: 5px;

      &_image {
        content: url("../assets/add_circle_outline-24px.svg");
        padding: 10px;
      }

      :hover {
        border-radius: 10px;
        transition: .5s;
        background-color: #9c9c9c;
      }
    }

    &_save {
      grid-area: save;
      display: grid;
      grid-auto-flow: column;
      justify-content: center;
      grid-gap: 20%;
      padding: 10px;
    }
  }
</style>

<script>
export default {
  name: "EditNote",
  components: {
    EditNoteContent: () => import('@/components/EditNoteContent.vue'),
    ButtonEditNote: () => import('@/components/ButtonEditNote.vue')
  },
  props: {
    id: {
      type: String,
      required: false
    }
  },
  computed: {
    getMethod () {
      if (this.id) return 'PUT'
      else return 'POST'
    }
  },
  data () {
    return {
      note: {
        id: null,
        title: '',
        todos: []
      }
    }
  },
  methods: {
    addTodo () {
      let id = -1
      if (this.note.todos.length > 0) id = this.note.todos[this.note.todos.length - 1].id
      this.note.todos.push({
        id: id + 1,
        title: '',
        completed: false
      })
    },
    changeTitle (newTitle) {
      this.note.title = newTitle
    },
    changeTodo (newTitle, todoId) {
      this.note.todos.find(todo => todo.id === todoId).title = newTitle
    },
    saveNote () {
      if (this.id) this.saveNoteFetch(this.id)
      else this.saveNoteFetch()
    },
    async onInit () {
      await fetch('http://localhost:3000/notes/' + this.id, {
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
          if (data) this.note = data
        })
        .catch(err => {
          console.log(err)
          this.error = err
        })
    },
    async saveNoteFetch (noteId = '') {
      await fetch('http://localhost:3000/notes/' + noteId, {
        method: this.getMethod,
        headers: {
          Accept: 'application/json',
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.note)
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
    if (this.id) this.onInit()
  }
}
</script>
