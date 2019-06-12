<template lang="pug">
section.container
  .ordering(
    :class="{ ordering_successed: orderingIsSuccessed, ordering_wrong: orderingIsWrong }")
    transition(name="fade")
      .h1.ordering__h1(v-if="orderingIsSuccessed")
        div Спасибо, что оставили заявку.
        div Мы скоро вам перезвоним.
      .p1.ordering__title(v-else) Оставьте заявку, и мы позвоним вам в ближайшее время
    form.ordering__form(novalidate @submit.prevent="sendOrdering")
      .ordering__phone-group
        the-mask.h1.ordering__phone(
          :class="getOrderingClass()"
          v-if="!orderingIsSuccessed"
          mask="+7 ### ### ####"
          autofocus
          placeholder="+7 ___ ___ ____"
          v-model="phone"
          @focus.native="resetOrderingStatus")
        .ordering__error-text.p2(v-if="orderingIsWrong") Проверьте набранный номер
      button.ordering__submit(type="submit" :disabled="orderingIsSuccessed")
        span Отправить заявку
        img.ordering__send-icon(:src="require('@/assets/svg/ic-send.svg')")
</template>

<script>
import axios from 'axios';
import { TheMask } from 'vue-the-mask';

export default {
  data: () => ({
    orderingStatus: '',
    phone: '',
  }),
  components: {
    TheMask,
  },
  computed: {
    orderingIsSuccessed() {
      return this.orderingStatus === 'success';
    },
    orderingIsWrong() {
      return this.orderingStatus === 'error';
    },
  },
  methods: {
    sendOrdering() {
      if (this.phone.length !== 10) {
        this.orderingStatus = 'error';
      } else {
        // TODO bind real data with payload
        axios.get('https://api.myjson.com/bins/cgjjh').then(() => {
          this.orderingStatus = 'success';
        }).catch(() => {
          this.orderingStatus = 'error';
        });
      }
    },
    resetOrderingStatus() {
      this.orderingStatus = '';
    },
    getOrderingClass() {
      return {
        ordering__phone_shadow: (this.phone.length && this.phone.length < 10),
        ordering__phone_filled: this.phone.length === 10,
        ordering__phone_wrong: this.orderingIsWrong,
      };
    },
  },
};
</script>
