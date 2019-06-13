<template lang="pug">
section.container.representation
  .representation__info
    .representation__title
      include ../assets/svg/ic-logo.svg
      include ../assets/svg/ic-title.svg
    .p1
      | Комплекс из камеры и мобильного приложения, который помогает в любой момент убедиться,
      | что с близкими и домом всё в порядке.
</template>

<style lang="scss" scoped>
section.representation {
  background: $color-atlantis url('~../assets/bg-representation.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  border: 1px solid $color-geyser;
  box-sizing: border-box;
  border-radius: 18px;
  padding: 38px 45px 45px;
  margin-bottom: 103px;
}
.representation {
  &__info {
    text-align: left;
    margin-right: 67%;
  }
  &__title {
    display: flex;
    align-items: center;
    margin-bottom: 39%;
    & svg:first-child {
      margin-right: 15px;
    }
  }
}
</style>
