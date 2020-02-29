<template>
  <div class="navbar">
    <router-link exact-active-class="navbar_home__active" class="navbar_home" to="/">
      <img class="navbar_home_image" src="@/assets/home-24px-white.svg">
    </router-link>
    <router-link exact-active-class="navbar_edit__active" class="navbar_edit" to="/about">
      <img class="navbar_home_image" src="@/assets/add_circle_outline-24px-white.svg">
    </router-link>
  </div>
</template>

<style lang="scss" scoped>
  .navbar {
    display: flex;
    flex-flow: column;
    position: absolute;
    left: 0;
    top: 0;
    width: 50px;
    height: 100%;
    background-color: #2c3e50;
    justify-content: center;
    align-items: center;
    margin: 0;
    padding: 0;

    &_home {
      width: inherit;
      display: flex;

      &_image {
        width: inherit;
      }

      &__active {
        background-color: #18222c;
      }

      :hover {
        transition: .5s;
        background-color: #18222c;
      }
    }

    &_edit {
      width: inherit;
      display: flex;

      &_image {
        width: inherit;
      }

      &__active {
        background-color: #18222c;
      }

      :hover {
        transition: .5s;
        background-color: #18222c;
      }
    }
  }
</style>

<script>
export default {
  name: "Navbar"
}
</script>
