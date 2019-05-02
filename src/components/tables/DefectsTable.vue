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
          {{ getToDate()[f] }}
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
      getToDate() {
        let toDate = {'planning': 0, 'design': 0, 'code': 0, compile: 0, test: 0};
        if (this.toDate != null) {
          this.toDate.forEach(d => {
            Object.keys(this.actual).forEach(fila => {
              toDate[fila] += parseInt(d[fila]);
            });
          });
          // Object.keys(this.actual).forEach(fila => {
          //     toDate[fila] += toDate[fila] + parseInt(this.actual[fila]);
          // });
          console.log(toDate);
          return toDate;
        } else {
          return undefined;
        }
      },
      total: function () {
        this.suma = {actual: 0, toDate: 0};
        Object.keys(this.actual).forEach(fila => {
          this.suma.actual += parseInt(this.actual[fila]);
        });
        if (this.toDate != null) {
          let toDate = this.getToDate()
          Object.keys(toDate).forEach(fila => {
            this.suma.toDate += parseInt(toDate[fila]);
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
