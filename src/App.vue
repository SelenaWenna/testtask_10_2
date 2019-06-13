<template lang="pug">
#app
  .good-modal__background(:class="{ 'good-modal__background_filtered': currentModal }")
    representation
    goods(@showModal="showModal")
    purchase
    ordering
    comments
  transition(name="fade")
    good-modal(
      v-if="currentModal"
      :content="currentModal"
      :sidePosition="sidePosition"
      @closeModal="closeModal")
</template>

<script>
import Representation from '@/components/Representation.vue';
import Goods from '@/components/Goods.vue';
import Purchase from '@/components/Purchase.vue';
import Ordering from '@/components/Ordering.vue';
import Comments from '@/components/Comments.vue';
import GoodModal from '@/components/GoodModal.vue';

export default {
  name: 'app',
  components: {
    Representation,
    Goods,
    Purchase,
    Ordering,
    Comments,
    GoodModal,
  },
  data: () => ({
    currentModal: null,
    sidePosition: '',
  }),
  methods: {
    showModal({ good, sidePosition }) {
      this.currentModal = good;
      this.sidePosition = sidePosition;
      document.body.classList.add('body_modal');
    },
    closeModal() {
      this.currentModal = null;
      this.sidePosition = '';
      document.body.classList.remove('body_modal');
    },
  },
};
</script>

<style lang="scss" scoped>
#app {
  font-family: $font-family-roboto;
  color: $color-shark;
}
.body_modal {
  overflow: hidden;
}
.container {
  max-width: 960px;
  min-width: 960px;
  margin: 0 auto;
  position: relative;
}
// Uikit
::v-deep {
  .h1 {
    font-family: $font-family-roboto-condensed;
    font-style: normal;
    font-weight: $font-weight-bold;
    font-size: 35px;
    line-height: 42px;
  }
  .h2 {
    font-family: $font-family-roboto-condensed;
    font-style: normal;
    font-weight: normal;
    font-size: 32px;
    line-height: 37px;
  }
  .p1 {
    font-style: normal;
    font-weight: bold;
    font-size: 20px;
    line-height: 23px;
  }
  .p2 {
    font-style: normal;
    font-weight: normal;
    font-size: 18px;
    line-height: 21px;
  }
}
</style>
