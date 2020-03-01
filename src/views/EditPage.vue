<template>
  <div class="about">
    <h1>Edit note: <span v-if="note">"{{ note.title }}"</span></h1>
    {{ note.title }}
  </div>
</template>

<style lang="scss" scoped>

</style>

<script>
export default {
  name: "EditPage",
  props: ["note"]
}
</script>
