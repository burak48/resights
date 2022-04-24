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
      :page.sync="page"
      :items-per-page="itemsPerPage"
      hide-default-footer
      @page-count="pageCount = $event"
    ).elevation-1.mt-10
    v-select(
      dense
      outlined
      hide-details
      :value="itemsPerPage"
      label="Items per page"
      @change="itemsPerPage = parseInt($event, 10)"
      :items="perPageChoices").mt-5
    v-pagination(v-model="page" :length="pageCount").mt-5
</template>

<script>
export default {
  props: ["headers", "items", "page", "itemsPerPage", "pageCount"],
  data() {
    return {
      search: "",
      perPageChoices: [
        { text: "5 records/page", value: 5 },
        { text: "10 records/page", value: 10 },
        { text: "20 records/page", value: 20 },
        { text: "40 records/page", value: 40 },
        { text: "80 records/page", value: 80 },
        { text: "100 records/page", value: 100 }
      ]
    };
  }
};
</script>

<style lang="sass" scoped>
.v-data-table
  max-width: 100%
</style>
