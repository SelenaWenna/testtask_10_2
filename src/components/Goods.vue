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
