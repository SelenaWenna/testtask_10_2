<template lang="pug">
  .good-modal
    .good-modal__wrapper(@click="$emit('closeModal')")
    .good-modal__content
      img.good-modal__close(
        :src="require('@/assets/svg/icon-close.svg')"
        :style="`${sidePosition}: -84px`"
        @click="$emit('closeModal')")
      .good-modal__item.p1(
        v-for="(item, index) in content"
        :key="index" :style="getBackground(item)"
        ) {{ item.text }}
</template>

<script>
export default {
  props: {
    content: {
      type: Array,
      default: () => [],
    },
    sidePosition: {
      type: String,
      default: 'right',
    },
  },
  methods: {
    getBackground(item) {
      return {
        backgroundImage: `url(${this.getUrl(item.icon)})`,
      };
    },
    getUrl(name) {
      const icons = require.context('@/assets/svg/', false);
      return icons(`./${name}`);
    },
  },
};
</script>

<style lang="scss">
.good-modal {
  background-color: rgba($color-mercury, 0.5);
  position: fixed;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  z-index: 10;
  display: flex;
  &__background {
    transition: filter $transition-duration;
    &_filtered {
      filter: grayscale(1);
    }
  }
  &__content {
    background: #fff;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    width: 75%;
    margin: auto;
    padding: 40px 40px 25px;
    box-sizing: border-box;
    background: linear-gradient(180deg, #8CB928 0%, #45AE4D 100%);
    border-radius: 18px;
    position: relative;
    max-width: 720px;
  }
  &__item {
    border-radius: 18px;
    width: 48.5%;
    height: 196px;
    margin-bottom: 15px;
    padding-left: 25.3%;
    padding-right: 18px;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    background-repeat: no-repeat;
    background-color: $color-white;
    background-position: -22% -50%;
  }
  &__close {
    position: absolute;
    top: calc(50% - 26px);
    cursor: pointer;
  }
  &__wrapper {
    position: absolute;
    width: 100%;
    height: 100%;
  }
}
.fade-enter-active, .fade-leave-active {
  transition: opacity $transition-duration;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
