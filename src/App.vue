<template>
  <div>
    <Table>
      <template #date="{ data: date = '-' }">
        {{ new Date(date).toLocaleDateString() }}
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
      return countries[value];
    },
  },
};
</script>

<style lang="scss"></style>
