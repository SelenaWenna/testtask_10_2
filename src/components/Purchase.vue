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

<style lang="scss" scoped>
.purchase {
  &__title {
    text-align: center;
    margin-bottom: 38px;
  }
  &__container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }
}
.option {
  text-align: center;
  color: $color-white;
  background: linear-gradient(180deg, #8CB928 0%, #45AE4D 100%);
  border-radius: 18px;
  width: calc((100% - 105px) / 4);
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding: 20px 0 18px;
  text-decoration: none;
  &__icon {
    margin-top: auto;
  }
  &__title {
    margin-top: 13px;
    margin-bottom: -4px;
    &_single {
      margin-top: 20px;
    }
  }
  &__subtitle {
    min-height: 16px;
  }
}
</style>
