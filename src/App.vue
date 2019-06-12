<template lang="pug">
#app
  .good-modal__background(:class="{ 'good-modal__background_filtered': currentModal }")
    representation
    goods(@showModal="showModal")
    purchase
    ordering
    comments
  transition(name="fade")
    good-modal(v-if="currentModal" :content="currentModal" :sidePosition="sidePosition" @closeModal="closeModal")
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
