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
