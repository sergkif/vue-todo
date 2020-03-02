<template>
  <div class="editPage">
    <EditNote :id="getId"/>
  </div>
</template>

<style lang="scss" scoped>
  .editPage {
    display: flex;
    justify-content: center;
  }
</style>

<script>
export default {
  name: "EditPage",
  components: {
    EditNote: () => import('@/components/EditNote.vue')
  },
  props: {
    id: {
      type: String,
      required: false
    }
  },
  computed: {
    getId () {
      if (this.id) return this.id.toString()
      else return ''
    }
  }
}
</script>
