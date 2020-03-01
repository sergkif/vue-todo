<template>
  <div class="noteHeader" :class="{ noteHeader__notModal: !isModal }">
    <div class="noteHeader_title">
      <h2>{{ title }}</h2>
    </div>
    <div class="noteHeader_editButton" v-if="isModal" @click="$emit('edit-note')"><img class="noteHeader_editButton_image"></div>
    <div class="noteHeader_deleteButton" v-if="isModal" @click="$emit('delete-note')"><img class="noteHeader_deleteButton_image"></div>
  </div>
</template>

<style lang="scss" scoped>
  .noteHeader {
    display: grid;
    grid-template-areas: "title edit delete";
    grid-auto-columns: 8fr 1fr 1fr;

    &__notModal {
      grid-template-areas: "title";
      grid-auto-columns: 8fr;
    }

    &_title {
      grid-area: title;
    }

    &_editButton {
      grid-area: edit;
      display: flex;

      &_image {
        content: url("../assets/edit-24px.svg");
        padding: 10px;
        width: stretch;
      }

      :hover {
        transition: .5s;
        background-color: #9c9c9c;
      }
    }

    &_deleteButton {
      grid-area: delete;
      display: flex;

      &_image {
        content: url("../assets/delete-24px.svg");
        padding: 10px;
        width: stretch;
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
  name: "NoteHeader",
  props: {
    title: {
      type: String,
      required: true
    },
    isModal: {
      type: Boolean,
      required: false,
      default: false
    }
  }
}
</script>
