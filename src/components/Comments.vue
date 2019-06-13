<template lang="pug">
  section.container.comments
    .h1.comments__title Отзывы
    .slider
      .slide(
        v-for="(comment, index) in comments"
        :class="getSlideClass(index)"
        :key="comment.id")
        .slide__img-circles
          img.slide__img(:src="require(`@/assets/${comment.userAvatar}`)")
        .slide__text
          .slide__username.p2 {{ comment.userFullname }}
          .p1 {{ comment.comment }}
      .slider__control-down(@click="showPrevComment")
        img(:src="require('@/assets/svg/ic-down.svg')")
</template>

<script>
const comments = [
  {
    commentId: 1,
    userAvatar: 'user-avatar.jpg',
    userFullname: 'Алексей Гоно',
    comment: 'Отличное и удобное приложение. Классные возможности, отзывчивая поддержка.',
  },
  {
    commentId: 2,
    userAvatar: 'user-avatar.jpg',
    userFullname: 'Андрей Иванов',
    comment: 'Отличное и удобное приложение.',
  },
  {
    commentId: 3,
    userAvatar: 'user-avatar.jpg',
    userFullname: 'Сергей Сидоров',
    comment: 'Классные возможности, отзывчивая поддержка.',
  },
];

export default {
  data: () => ({
    currentCommentIndex: 0,
    comments,
  }),
  computed: {
    prevCommentIndex() {
      const prevCommentIndex = this.currentCommentIndex - 1;
      return prevCommentIndex < 0 ? this.comments.length - 1 : prevCommentIndex;
    },
  },
  methods: {
    showPrevComment() {
      this.currentCommentIndex = this.prevCommentIndex;
    },
    getSlideClass(index) {
      return {
        slide_current: index === this.currentCommentIndex,
        slide_prev: index === this.prevCommentIndex,
      };
    },
  },
};
</script>

<style lang="scss" scoped>
.comments {
  &__title {
    text-align: center;
    margin-bottom: 73px;
  }
}
.slider {
  width: 58%;
  min-width: 560px;
  margin: 0 auto;
  position: relative;
  &__control-down {
    position: absolute;
    bottom: 13px;
    right: calc(50% - 7px);
    left: calc(50% - 7px);
    cursor: pointer;
  }
}
.slide {
  opacity: 0;
  position: absolute;
  top: 0;
  height: 240px;
  width: 100%;
  transition: all $transition-duration;
  display: none;
  overflow: hidden;
  color: $color-white;
  padding: 20px 19px;
  box-sizing: border-box;
  &_current,
  &_prev {
    display: flex;
    background: linear-gradient(180deg, #8CB928 0%, #45AE4D 100%);
    border-radius: 18px;
  }
  &_current {
    position: relative;
    opacity: 1;
    box-sizing: border-box;
  }
  &_prev {
    opacity: 0.5;
    position: absolute;
    top: -50px;
    transform: scale(0.83);
    z-index: -1;
  }
  &__img {
    width: 100%;
    height: 100%;
    border-radius: 50%;
  }
  &__img-circles {
    width: 102px;
    height: 102px;
    border: 1px solid rgba($color-white, 0.25);
    border-radius: 50%;
    padding: 12px;
    box-sizing: border-box;
    position: relative;
    flex-shrink: 0;
    margin-right: 20px;
    &::before,
    &::after {
      content: '';
      border-radius: 50%;
      position: absolute;
    }
    &::before {
      border: 1px solid rgba($color-white, 0.5);
      top: 4px;
      right: 4px;
      left: 4px;
      bottom: 4px;
    }
    &::after {
      border: 1px solid $color-white;
      top: 8px;
      right: 8px;
      left: 8px;
      bottom: 8px;
    }
  }
  &__username {
    margin-top: 40px;
    margin-bottom: 22px;
  }
}
</style>

