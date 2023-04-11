<template>
  <div class="bar">
    <div class="bar__inputs">
      <v-select
          v-model="gender"
          :items="['male', 'female', 'unknown', 'genderless']"
          multiple
          label="Gender"
          background-color="#fff"
          color="#000"
          class="bar__input"
          @change="$emit('onFilterChange', {name: 'gender', value: gender})"
      ></v-select>

      <v-select
          v-model="status"
          :items="['alive', 'dead', 'unknown']"
          multiple
          label="Status"
          background-color="#fff"
          color="#000"
          class="bar__input"
          @change="$emit('onFilterChange', {name: 'status', value: status})"
      ></v-select>

      <v-text-field
          v-model="name"
          :counter="10"
          label="Search"
          background-color="#fff"
          color="#000"
          class="bar__input"
          required
          @input="$emit('onFilterChange', {name: 'name', value: name})"
      ></v-text-field>
    </div>

    <v-btn @click="$emit('openFilters')">
      <v-icon>mdi-filter</v-icon>
    </v-btn>
  </div>
</template>

<script>
  export default {
    name: 'AppBar',

    data: () => ({
      gender: [],
      status: [],
      name: ''
    }),
  }
</script>

<style lang="scss">
.bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0px 20px;
  background: #777777;
  &__inputs {
    display: flex;
    gap: 25px;
    color: #fff;
  }
  &__input {
    max-width: 265px;
    input, label, .v-select__selections {
      padding-left: 5px !important;
    }
  }
}
</style>
