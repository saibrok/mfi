<template>
  <table class="table">
    <thead>
      <tr>
        <th
          v-for="column in columns"
          :key="column.id"
          @click="toggleSort(column.id)"
        >
          <div class="th-content">
            {{ column.caption }}
            <div v-if="sortingOptions[column.id]" class="arrow">
              <template v-if="sortingOptions[column.id] === 1">▲</template>
              <template v-if="sortingOptions[column.id] === -1">▼</template>
            </div>
          </div>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(row, index) in sortedRows" :key="index">
        <td v-for="column in columns" :key="column.id">
          <slot :name="column.template" v-bind:data="row[column.id]">
            {{ row[column.id] }}
          </slot>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "Table",
  data() {
    return {
      columns: [
        { caption: "ФИО", id: "fio" },
        { caption: "Дата рождения", id: "dob", template: "date" },
        { caption: "Страна проживания", id: "country", template: "country" },
      ],

      rows: [
        { fio: "Райли Рид", dob: 730166400, country: "us" },
        { fio: "Лоза Юрий Эдуардович", dob: -502243200, country: "ru" },
        { fio: "Меркель Ангела", dob: -487900800, country: "de" },
        { fio: "Назарбаев Нурсултан Абишевич", dob: -930614400, country: "kz" },
      ],
      sortableСolumn: "",

      sortingOptions: {
        fio: 0,
        dob: 0,
        country: 0,
      },
    };
  },

  computed: {
    sortedRows() {
      const sortedRows = [...this.rows];
      return sortedRows.sort(
        this.sortByField(
          this.sortableСolumn,
          this.sortingOptions[this.sortableСolumn]
        )
      );
    },
  },

  mounted() {
    if (localStorage.sortableСolumn) {
      this.sortableСolumn = localStorage.sortableСolumn;
    }
    if (localStorage.sortingOptions) {
      this.sortingOptions = JSON.parse(localStorage.sortingOptions);
    }
  },

  methods: {
    toggleSort(id) {
      if (this.sortableСolumn !== id) {
        this.sortingOptions = {
          fio: 0,
          dob: 0,
          country: 0,
        };

        localStorage.sortingOptions = JSON.stringify(this.sortingOptions);
        localStorage.sortableСolumn = this.sortableСolumn = id;
      }

      this.sortingOptions[this.sortableСolumn] >= 1
        ? (this.sortingOptions[this.sortableСolumn] = -1)
        : (this.sortingOptions[this.sortableСolumn] += 1);

      localStorage.sortingOptions = JSON.stringify(this.sortingOptions);
    },

    sortByField(field, direction) {
      return (a, b) => (a[field] > b[field] ? 1 * direction : -1 * direction);
    },
  },
};
</script>

<style scoped lang="scss">
.th-content {
  display: flex;
  justify-content: space-between;
  cursor: pointer;
}

// sample table styles
.table {
  width: 100%;
  border: none;
  margin-bottom: 20px;
  border-collapse: separate;
}
.table thead th {
  font-weight: bold;
  text-align: left;
  border: none;
  padding: 10px 15px;
  background: #ededed;
  font-size: 14px;
  border-top: 1px solid #dddddd;
}
.table tr th:first-child,
.table tr td:first-child {
  border-left: 1px solid #dddddd;
}
.table tr th:last-child,
.table tr td:last-child {
  border-right: 1px solid #dddddd;
}
.table thead tr th:first-child {
  border-radius: 20px 0 0 0;
}
.table thead tr th:last-child {
  border-radius: 0 20px 0 0;
}
.table tbody td {
  text-align: left;
  border: none;
  padding: 10px 15px;
  font-size: 14px;
  vertical-align: top;
}
.table tbody tr:nth-child(even) {
  background: #f8f8f8;
}
.table tbody tr:last-child td {
  border-bottom: 1px solid #dddddd;
}
.table tbody tr:last-child td:first-child {
  border-radius: 0 0 0 20px;
}
.table tbody tr:last-child td:last-child {
  border-radius: 0 0 20px 0;
}
</style>
