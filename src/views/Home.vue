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
  name: 'Home',
  components: {
    NoteList: () => import('@/components/NoteList.vue')
  }
}
</script>
