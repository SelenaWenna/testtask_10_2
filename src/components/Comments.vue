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
