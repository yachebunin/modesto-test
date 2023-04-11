<template>
  <div class="card">
    <img class="card__img" :src="character.image" :alt="character.name">
    <div class="card__title">{{ character.name }}</div>
    <div class="card__gender card__text">Gender: <span>{{ character.gender }}</span></div>
    <div class="card__status card__text">Status: <span>{{ character.status }}</span></div>
    <div class="card__location card__text">Location: <span>{{ character.location?.name }}</span></div>
  </div>
</template>

<script>
export default {
  name: 'AppCard',

  props: ['character'],

  data: () => ({
  }),
}
</script>

<style lang="scss">
.card {
  flex-basis: 18%;
  padding: 20px;
  background: #777777;
  border-radius: 5px;
  font-family: 'PT Sans';
  line-height: 18px;
  color: #FFFFFF;
  &__img {
    max-width: 100%;
  }
  &__title {
    margin-bottom: 7px;
    font-weight: 700;
    font-size: 14px;
  }
  &__text {
    font-weight: 400;
    font-size: 12px;
    line-height: 16px;
  }
}
</style>
