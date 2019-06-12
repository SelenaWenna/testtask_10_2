<template lang="pug">
section.container.purchase
  .h1.purchase__title Приобрести
  .purchase__container
    a.option(href="#" v-for="(option, index) in purchaseOptions" :key="index")
      img.option__icon(:src="require(`@/assets/svg/${option.icon}`)")
      .option__title.p1(
        :class="{ option__title_single: !option.subtitle }"
        ) {{ option.title }}
      .option__subtitle.p1 {{ option.subtitle }}
</template>

<script>
export default {
  name: 'purchase',
  data: () => ({
    purchaseOptions: [
      {
        icon: 'icon-cam.svg',
        title: 'Покупка',
      },
      {
        icon: 'icon-ras.svg',
        title: 'Рассрочка',
      },
      {
        icon: 'icon-control.svg',
        title: 'Пакет',
        subtitle: '“Все под контролем”',
      },
      {
        icon: 'icon-1500.svg',
        title: 'Пакет',
        subtitle: '“Тысяча пятьсот”',
      },
    ],
  }),
};
</script>
