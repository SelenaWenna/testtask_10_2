<template lang="pug">
section.container.goods
  .goods__item(v-for="(good, index) in goods" :key="index")
    .goods__img
      img(:src="require('@/assets/cam.png')")
    button.p1.goods__detail(
      @click="$emit('showModal', { good, sidePosition: (index ? 'right' : 'left') })"
      ) Подробнее
</template>

<script>
export default {
  data: () => ({
    goods: [
      [
        {
          icon: 'ic-wifi.svg',
          text: 'Работает по Wi-Fi или кабелю',
        },
        {
          icon: 'ic-resolution.svg',
          text: 'Разрешение 1280х960 (HD)',
        },
        {
          icon: 'ic-night.svg',
          text: 'Ночная съемка',
        },
        {
          icon: 'ic-record.svg',
          text: 'Запись звука и видео',
        },
        {
          icon: 'ic-angle.svg',
          text: 'Угол обзора 100°',
        },
        {
          icon: 'ic-cable.svg',
          text: 'Длина кабеля 1.5 метра',
        },
      ],
      [
        {
          icon: 'ic-move.svg',
          text: 'Уведомление на телефон о движении',
        },
        {
          icon: 'ic-server.svg',
          text: 'Хранение данных на защищенных серверах',
        },
        {
          icon: 'ic-access.svg',
          text: 'Совместный доступ у членов семьи',
        },
        {
          icon: 'ic-archive.svg',
          text: 'Скачивание/удаление архивных записей',
        },
        {
          icon: 'ic-geo.svg',
          text: 'Доступ из любой точки мира',
        },
        {
          icon: 'ic-notifications.svg',
          text: 'Уведомление о приходе «Домашних»',
        },
      ],
    ],
  }),
};
</script>

<style lang="scss" scoped>
section.goods {
  display: flex;
  margin-bottom: 70px;
}
.goods {
  &__item {
    position: relative;
    width: calc(50% - 90px);
    margin-right: 4.69%;
    margin-left: 4.69%;
    text-align: center;
  }
  &__img {
    padding: 80px 90px 77px;
    background: $color-atlantis linear-gradient(180deg, #8CB928 0%, #45AE4D 100%);
    border-radius: 18px;
    box-sizing: border-box;
    position: relative;
    &::before {
      content: '';
      display: block;
      height: 100%;
      position: absolute;
      top: 0;
      left: 12%;
      right: 12%;
      box-shadow: 0px 25px 100px #48AE4B;
      border-radius: 18px;
      box-sizing: border-box;
      z-index: -1;
    }
  }
  &__detail {
    text-transform: uppercase;
    letter-spacing: 2px;
    background: transparent;
    border: none;
    margin-top: 15px;
    cursor: pointer;
    &:focus {
      outline: none;
    }
  }
}
</style>
