<template>
  <div data-app>
    <AppBar @onFilterChange="onFilterChange" @openFilters="visibleFilters(true)" />
    <AppBody :characters="characters"/>
    <AppPagination :info="characters?.info" @onFilterChange="onFilterChange" />
    <transition name="fade">
      <AppFilters
          :isOpenedFilters="isOpenedFilters"
          @onFilterChange="onFilterChange"
          @closeFilters="visibleFilters(false)"
      />
    </transition>

    <div v-if="isOpenedFilters" @click="visibleFilters(false)" class="black-window"></div>
  </div>
</template>

<script>
import AppBody from './components/AppBody';
import AppBar from './components/AppBar'
import AppPagination from './components/AppPagination'
import AppFilters from './components/AppFilters'

export default {
  name: 'App',

  components: {
    AppBody,
    AppBar,
    AppPagination,
    AppFilters
  },

  data: () => ({
    characters: [],
    filters: {
      gender: '',
      status: '',
      name: '',
      page: 1
    },
    isOpenedFilters: false
  }),

  created () {
    this.getCharacters()
  },

  methods: {
    async getCharacters () {
      const {
        page = 1,
        name = '',
        gender = '',
        status = '',
      } = this.filters || {}
      const response =
          await fetch(`https://rickandmortyapi.com/api/character/?page=${page}&name=${name}&gender=${gender}&status=${status}`)
      this.characters = await response.json()
    },
    onFilterChange({name, value}) {
      this.filters[name] = Array.isArray(value) ? value.join('&') : value
      if (name !== 'page') this.filters.page = 1

      this.getCharacters()
      this.visibleFilters(false)
    },
    visibleFilters(value) {
      this.isOpenedFilters = value
    }
  }
};
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
.black-window {
  position: fixed;
  left: 0px;
  top: 0px;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
}
</style>
