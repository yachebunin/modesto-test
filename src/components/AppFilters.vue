<template>
  <div v-if="isOpenedFilters" class="filters">
      <v-icon @click="$emit('closeFilters')" class="filters__close">mdi-close</v-icon>

      <div class="filters__title">All filters</div>

      <v-text-field
          v-model="name"
          :counter="10"
          label="Search"
          background-color="#fff"
          color="#000"
          class="bar__input"
          required
      ></v-text-field>

      <div class="filters__block block">
        <div @click="changeVisibleBlock('gender')" class="block__title">
          <span>Gender</span>
          <v-icon v-if="openedFilters.indexOf('gender') === -1">mdi-arrow-right</v-icon>
          <v-icon v-else>mdi-arrow-down</v-icon>
        </div>

        <div v-if="openedFilters.indexOf('gender') !== -1" class="filters__list">
          <div
              v-for="(gender, index) in getGenders"
              :key="gender.name"
              @click="selectGender(gender, index)"
              class="filters__element"
          >
            <input
                type="checkbox"
                :checked="gender.isActive"
            />
            <span>{{ gender.name }}</span>
          </div>
        </div>
      </div>

      <div class="filters__block block">
        <div @click="changeVisibleBlock('status')" class="block__title">
          <span>Status</span>
          <v-icon v-if="openedFilters.indexOf('status') === -1">mdi-arrow-right</v-icon>
          <v-icon v-else>mdi-arrow-down</v-icon>
        </div>

        <div v-if="openedFilters.indexOf('status') !== -1" class="filters__list">
          <div
              v-for="(status, index) in getStatuses"
              :key="status.name"
              @click="selectStatus(status, index)"
              class="filters__element"
          >
            <input
                type="checkbox"
                :checked="status.isActive"
            />
            <span>{{ status.name }}</span>
          </div>
        </div>
      </div>

      <div class="filters__buttons">
        <button @click="clearFilters" class="filters__button filters__clear">Clear all</button>
        <button
            @click="changeFilter"
            class="filters__button filters__apply"
        >Apply</button>
      </div>
    </div>
</template>

<script>
import Vue from 'vue'

export default {
  name: 'AppFilters',

  props: ['isOpenedFilters'],

  data: () => ({
    genders: [
      {name: 'male', isActive: false},
      {name: 'female', isActive: false},
      {name: 'unknown', isActive: false},
      {name: 'genderless', isActive: false},
    ],
    statuses: [
      {name: 'alive', isActive: false},
      {name: 'dead', isActive: false},
      {name: 'unknown', isActive: false},
    ],
    selectedGenders: [],
    selectedStatuses: [],
    openedFilters: [],
    name: ''
  }),

  methods: {
    changeVisibleBlock(name) {
      if (this.openedFilters.indexOf(name) === -1) {
        this.openedFilters.push(name)
        return
      }

      this.openedFilters = this.openedFilters.filter((el) => el !== name)
    },
    selectGender(gender, index) {
      if (this.selectedGenders.indexOf(gender.name) === -1) {
        this.selectedGenders.push(gender.name)
      } else {
        this.selectedGenders = this.selectedGenders.filter((el) => el !== gender.name)
      }
      gender.isActive = !gender.isActive
      Vue.set(this.genders, index, gender)
    },
    selectStatus(status, index) {
      if (this.selectedStatuses.indexOf(status.name) === -1) {
        this.selectedStatuses.push(status.name)
      } else {
        this.selectedStatuses = this.selectedStatuses.filter((el) => el !== status.name)
      }
      status.isActive = !status.isActive
      Vue.set(this.statuses, index, status)
    },
    clearFilters() {
      this.selectedStatuses = []
      this.selectedGenders = []

      this.genders.forEach((gender) => {
        gender.isActive = false
      })
      this.statuses.forEach((status) => {
        status.isActive = false
      })

      this.name = ''
    },
    changeFilter() {
      if (this.name !== '') {
        this.$emit('onFilterChange', {name: 'name', value: this.name})
      }
      if (this.selectedGenders.length) {
        this.$emit('onFilterChange', {name: 'gender', value: this.selectedGenders})
      }
      if (this.selectedStatuses.length) {
        this.$emit('onFilterChange', {name: 'status', value: this.selectedStatuses})
      }
    }
  },

  computed: {
    getStatuses() {
      return this.statuses
    },
    getGenders() {
      return this.genders
    }
  }
}
</script>

<style lang="scss">
.filters {
  position: fixed;
  right: 0px;
  top: 0px;
  min-width: 20%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  padding: 40px 20px;
  background: #FFFFFF;
  z-index: 10000;
  &__close {
    position: absolute !important;
    right: 20px;
    top: 20px;
    cursor: pointer;
  }
  .v-input {
    flex: none;
  }
  &__title {
    font-family: 'PT Sans';
    font-style: normal;
    font-weight: 700;
    font-size: 24px;
    line-height: 26px;
    text-align: center;
    color: #000000;
  }
  .block {
    &__title {
      display: flex;
      align-items: center;
      font-family: 'PT Sans';
      font-style: normal;
      font-weight: 400;
      font-size: 18px;
      line-height: 22px;
      color: #000000;
      cursor: pointer;
      span {
        margin-right: 10px;
      }
    }
    .v-input--selection-controls {
      margin-top: 0px;
      .v-input__slot {
        margin-bottom: 0px;
      }
    }
  }
  &__element {
    display: flex;
    align-items: center;
    gap: 10px;
    cursor: pointer;
  }
  &__buttons {
    display: flex;
    justify-content: space-between;
    align-items: center;
    min-width: 100%;
    gap: 20px;
    margin-top: auto;
  }
  &__button {
    background: #F2F2F1;
    border: 1px solid #D8D8D8;
    border-radius: 5px;
    flex-basis: 50%;
    padding: 5px 0px;
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 18px;
  }
  &__clear {
    background: #F2F2F1;
  }
  &__apply {
    background: #FFE607;
  }
}
</style>
