<template>
  <div class="homePage">
    <NoteList />
  </div>
</template>

<style lang="scss" scoped>
  .homePage {
    display: flex;
    justify-content: center;
  }
</style>

<script>
export default {
  name: 'HomePage',
  components: {
    NoteList: () => import('@/components/NoteList.vue')
  }
}
</script>
