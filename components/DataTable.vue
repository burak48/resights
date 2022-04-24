<template lang="pug">
  div
    v-text-field(
      v-model="search"
      append-icon="mdi-magnify"
      label="Search"
      single-line
      hide-details
    )
    v-data-table(
      :headers="headers"
      :items="items"
      item-key="email"
      dense
      sort-by="gender"
      :search="search"
    ).elevation-1.mt-10
</template>

<script>
export default {
  props: ["headers", "items"],
  data() {
    return {
      search: ""
    };
  }
};
</script>

<style lang="sass" scoped>
.v-data-table
  max-width: 100%
</style>
