<template lang="pug">
  v-container
    v-row
      v-col(cols)
        DataTable(
          v-if="items.length"
          :headers="headers"
          :items="items"
        )
        v-progress-circular(
          v-else
          width="2"
          color="rs__primary"
          indeterminate
        ).mx-auto
</template>

<script>
import DataTable from "~/components/DataTable.vue";
import sales from "~/api/sales.js";

export default {
  components: {
    DataTable
  },
  data() {
    return {
      sales,
      items: [],
      headers: [
        { text: "Name", value: "user", align: "start", width: "180px" },
        { text: "Email", value: "email", width: "300px" },
        { text: "Gender", value: "gender", width: "180px" },
        { text: "Year", value: "year", width: "180px" },
        { text: "Sales", value: "sales", width: "180px" },
        { text: "Country", value: "country", width: "180px" }
      ]
    };
  },
  async created() {
    this.items = await this.fetchData(0, 50);
  },
  methods: {
    async fetchData(page, size) {
      const start = page * size;
      await this.delay(3000);
      return await sales.results.slice(start, start + size);
    },
    delay(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    }
  }
};
</script>

<style lang="sass" scoped>
.v-progress-circular
  position: absolute
  top: 50%
  left: 50%
</style>
