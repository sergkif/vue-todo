<template>
  <div class="home">
    <NoteList />
  </div>
</template>

<style lang="scss" scoped>
  .home {
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
