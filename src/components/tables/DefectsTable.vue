<template>
  <form @input="total(); $emit('actualizado')">
    <table border="1">
      <thead>
      <th>{{ titulo }}</th>
      <td v-for="c in columnas">
        {{ c }}
      </td>
      </thead>
      <tbody>
      <tr v-for="f in filas">
        <th>{{ f }}</th>
        <!--actual-->
        <td v-if="!serializar">
          <input type="text" v-model="actual[f]">
        </td>
        <td v-if="serializar">
          {{ actual[f] }}
        </td>
        <!--to date-->
        <td v-if="toDate != null">
          {{ parseInt(toDate[f]) + parseInt(actual[f]) }}
        </td>
        <td v-if="toDate == null">
          {{ actual[f] }}
        </td>
      </tr>
      <tr>
        <th>Total</th>
        <td>{{ suma.actual }}</td>
        <td>{{ suma.toDate }}</td>
      </tr>
      </tbody>
    </table>
  </form>
</template>

<script>
  export default {
    name: "InputTable",
    props: ['titulo', 'actual', 'toDate', 'suma'],
    data() {
      return {
        serializar: false,
        valores: [],
        filas: ['planning', 'design', 'code', 'compile', 'test'],
        columnas: ['actual', 'to date'],
      }
    },
    methods: {
      total: function () {
        this.suma = {actual: 0, toDate: 0};
        Object.keys(this.actual).forEach(fila => {
          this.suma.actual += parseInt(this.actual[fila]);
        });
        if (this.toDate != null) {
          Object.keys(this.toDate).forEach(fila => {
            this.suma.toDate += parseInt(this.toDate[fila]) + parseInt(this.actual[fila]);
          });
        } else {
          this.suma.toDate = this.suma.actual;
        }
      }
    },
  }
</script>

<style scoped>

</style>
