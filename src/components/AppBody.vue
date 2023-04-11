<template>
  <div class="list">
    <AppCard
      v-for="character in getCharacters"
      :key="character.id"
      :character="character"
    />
  </div>
</template>

<script>
import AppCard from './AppCard'

  export default {
    name: 'AppBody',

    data: () => ({
    }),

    props: ['characters'],

    computed: {
      getCharacters() {
        return this.characters?.results
      }
    },

    components: {
      AppCard
    }
  }
</script>

<style lang="scss">
.list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  gap: 20px;
  padding: 20px;
}
</style>
