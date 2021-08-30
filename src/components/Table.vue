<template>
  <table class="table">
    <thead>
      <tr>
        <th v-for="column in columns" :key="column.id">{{ column.caption }}</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(row, index) in rows" :key="index">
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
    };
  },
};
</script>

<style scoped lang="scss">
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
