<template>
  <div class="buttonEditNote" :style="{ 'color': color, 'border': '2px solid ' + color }" @click="$emit('click')">
    <div class="buttonEditNote_underline" :style="{ 'background': color }"></div>
    <span class="buttonEditNote_title" :style="{ 'color': color }">{{ buttonLabel }}</span>
  </div>
</template>

<style lang="scss" scoped>
  .buttonEditNote {
    display: inline-flex;
    position: relative;
    height: 40px;
    width: 150px;
    text-transform: uppercase;
    text-decoration: none;
    font-size: .8em;
    letter-spacing: 1.5px;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    cursor: pointer;

    &_title {
      text-decoration: none;
      letter-spacing: 1px;
    }

    &_underline {
      width: 100%;
      height: 2.5px;
      margin-top: 15px;
      align-self: flex-end;
      left: -200px;
      position: absolute;
      transition: all .3s ease-Out;
      bottom: 0;
    }

    &:hover .buttonEditNote_underline {
      left: 0;
    }

    .buttonEditNote_title {
      position: relative;
      transition: all .45s ease-Out;
    }
  }
</style>

<script>
export default {
  name: "ButtonEditNote",
  props: {
    color: {
      type: String,
      required: false,
      default: '#BFC0C0'
    },
    buttonLabel: {
      type: String,
      required: true
    }
  }
}
</script>
