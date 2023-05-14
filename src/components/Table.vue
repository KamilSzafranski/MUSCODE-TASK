<template>
  <li>
    <h4 class="title">Lista Produktów</h4>
    <table class="tab">
      <thead>
        <tr class="row">
          <th>#</th>
          <th>NAZWA</th>
          <th>PROMOCYJNA CENA</th>
          <th>CENA</th>
          <th>WALUTA</th>
        </tr>
      </thead>

      <tbody>
        <tr class="row" v-for="(product, index) in products">
          <td>{{ index }}</td>
          <td>{{ product.name }}</td>
          <td>{{ product.salePrice }}</td>
          <td>{{ product.price }}</td>
          <td>{{ product.currency }}</td>
        </tr>
      </tbody>
    </table>
  </li>
</template>
<script>
export default {
  props: ["products"],
  mounted() {},
};
</script>
<style scoped>
.title {
  margin-bottom: 20px;
}
.tab {
  width: 100%;

  font-size: 12px;
  border-collapse: collapse;
}

.title {
  color: var(--var-title-color);
}
.row {
  border-bottom: 0.5px var(--var-btn-border-color) solid;
}
td {
  padding: 5px;
}
th {
  padding: 5px;
  cursor: pointer;
}

tr:hover {
  background-color: var(--var-bg);
}

thead th:nth-child(1),
tbody th:nth-child(1) {
  width: 10%;
}

thead th:nth-child(2) tbody th:nth-child(2) {
  width: 40%;
}

thead th:nth-child(3),
tbody th:nth-child(3) {
  width: 20%;
}

thead th:nth-child(4),
tbody th:nth-child(4) {
  width: 15%;
}
thead th:nth-child(5),
tbody th:nth-child(5) {
  width: 15%;
}
</style>
