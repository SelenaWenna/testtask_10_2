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

<style lang="scss" scoped>
.ordering {
  padding: 41px;
  background: #FFFFFF;
  border-radius: 18px;
  width: 82%;
  margin: 110px auto 123px;
  text-align: center;
  position: relative;
  &::before {
    content: '';
    transition: opacity $transition-duration;
    height: 100%;
    display: block;
    position: absolute;
    top: 0;
    right: 5%;
    left: 5%;
    background: linear-gradient(180deg, #8CB928 0%, #45AE4D 100%);
    box-shadow: 0px 25px 100px #48AE4B;
    border-radius: 18px;
    z-index: -1;
  }
  &__h1 {
    margin-top: 43px;
    margin-bottom: 48px;
    line-height: 47px;
  }
  &__title {
    width: 45%;
    margin: 0 auto 35px;
    text-align: center;
  }
  &__phone {
    border: 3px solid $color-geyser;
    border-radius: 4px;
    display: block;
    width: 100%;
    padding: 10px 15px 5px 21px;
    box-sizing: border-box;
    transition: all $transition-duration;
    &:focus {
      border-color: $color-apple;
    }
    &_shadow {
      border-color: $color-apple;
      box-shadow: 0px 24px 24px rgba(0, 152, 16, 0.25), 0px 0px 24px rgba(0, 152, 16, 0.25);
    }
    &_filled {
      border-color: $color-apple;
    }
    &_wrong {
      border-color: $color-crail;
      color: $color-crail;
    }
  }
  &__phone-group {
    position: relative;
    width: 276px;
    margin: 0 auto 41px;
  }
  &__error-text {
    position: absolute;
    bottom: -28px;
    white-space: nowrap;
    &::before {
      content: '!';
      width: 21px;
      height: 21px;
      border-radius: 50%;
      color: white;
      background-color: $color-crail;
      display: inline-block;
      margin-right: 10px;
    }
  }
  &__submit {
    font-family: $font-family-roboto-condensed;
    font-style: normal;
    font-weight: $font-weight-bold;
    font-size: 22px;
    line-height: 26px;
    text-transform: uppercase;
    color: $color-white;

    cursor: pointer;
    background: $color-sushi;
    border-radius: 4px;
    position: relative;
    display: inline-flex;
    align-items: center;
    padding: 18px 16px 15px 20px;
    margin-bottom: 5px;
    transition: background-color $transition-duration;
    &::before {
      content: '';
      display: block;
      position: absolute;
      top: 100%;
      bottom: -6px;
      right: 10px;
      left: 10px;
      background: $color-japanese-laurel;
      border-radius: 0 0 4px 4px;
      transition: opacity $transition-duration;
    }
    &[disabled] {
      background: $color-geyser;
      &::before {
        opacity: 0;
      }
    }
  }
  &__send-icon {
    margin-left: 8px;
    margin-top: -2px;
  }
  &_successed {
    &::before {
      opacity: 0;
    }
  }
}
</style>
