<template>
  <div>
    <Table>
      <template #date="{ data: date = '-' }">
        {{
          new Date(date * 1000).toLocaleString("ru", {
            year: "numeric",
            month: "long",
            day: "numeric",
          })
        }}
      </template>
      <template #country="{ data: country = '-' }">
        {{ country | countryName(countries) }}
      </template>
    </Table>
  </div>
</template>

<script>
import Table from "./components/Table.vue";

export default {
  name: "App",

  components: {
    Table,
  },

  data() {
    return {
      countries: {
        us: "США",
        ru: "Россия",
        de: "Германия",
        kz: "Казахстан",
        fr: "Франция",
        by: "Беларусь",
        au: "Австралия",
      },
    };
  },

  computed: {
    name() {
      return this.countries;
    },
  },

  filters: {
    countryName(value, countries) {
      return countries[value.toLowerCase()];
    },
  },
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}
</style>
