<template>
  <div class="editInput">
    <input class="editInput_title" :placeholder="noteKey" v-model="noteValue" type="input" :name="noteKey + id" :id="noteKey + id" required>
    <label v-if="noteKey == 'Todo' && id" :for="noteKey + id" class="editInput_label">{{noteKey + ' ' + id}}</label>
    <label v-else :for="noteKey + id" class="editInput_label">{{noteKey}}</label>
    <div class="editInput_delete" v-if="noteKey == 'Todo'">
      <img class="editInput_delete_image">
    </div>
  </div>
</template>

<style lang="scss" scoped>
  $primary: #2c3e50;
  $secondary: #555;
  $gray: #9b9b9b;

  .editInput {
    display: grid;
    grid-template-areas: "title delete";
    grid-template-columns: 7fr 1fr;
    position: relative;
    padding: 15px 0 0;

    &_title {
      font-family: inherit;
      width: 100%;
      border: 0;
      border-bottom: 2px solid $gray;
      outline: 0;
      font-size: 1.3rem;
      padding: 7px 0;
      background: transparent;
      transition: border-color 0.2s;

      &::placeholder {
        color: transparent;
      }

      &:placeholder-shown ~ .editInput_label {
        font-size: 1.3rem;
        cursor: text;
        top: 20px;
      }

      &:required,&:invalid { box-shadow:none; }
    }

    &_label {
      position: absolute;
      top: 0;
      display: block;
      transition: 0.2s;
      font-size: 1rem;
      color: $gray;
    }

    &_title:focus {
        ~ .editInput_label {
          position: absolute;
          top: 0;
          display: block;
          transition: 0.2s;
          font-size: 1rem;
          color: $primary;
          font-weight:700;    
        }

        ~ .editInput_delete {
          border-bottom: 2.5px solid $secondary;
          font-weight: 700;
        }

        padding-bottom: 6px;  
        font-weight: 700;
        border-width: 3px;
        border-image: linear-gradient(to right, $primary,$secondary);
        border-image-slice: 1;
      }

    &_delete {
      grid-area: delete;
      display: flex;
      border-bottom: 2px solid $gray;

      &_image {
        content: url("../assets/delete-24px.svg");
        padding: 10px;
      }

      :hover {
        transition: .5s;
        background-color: #9c9c9c;
      }
    }
  }
</style>

<script>
export default {
  name: "EditInput",
  props: {
    noteKey: {
      type: String,
      required: true
    },
    noteValueProps: {
      type: String,
      required: false,
      default: ''
    },
    id: {
      type: String,
      required: false
    }
  },
  data () {
    return {
      noteValue: this.noteValueProps
    }
  },
  methods: {
    deleteTodo(todoId) {
      this.$emit('delete-todo', todoId)
    }
  },
  watch: {
    noteValue: function (noteValue) {
      if(this.id) this.$emit('data-changed', noteValue, this.id)
      else this.$emit('data-changed', noteValue)
    }
  }
}
</script>
