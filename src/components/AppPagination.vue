<template>
  <v-pagination
      v-if="info"
      v-model="page"
      :length="info?.pages"
      @input="onFilterChange"
  ></v-pagination>
</template>

<script>
  export default {
    name: 'AppPagination',

    props: ['info'],

    data: () => ({
      page: 1,
    }),

    methods: {
      onFilterChange(page) {
        this.$emit('onFilterChange', {name: 'page', value: page})
      }
    }
  }
</script>

<style lang="scss">
</style>
