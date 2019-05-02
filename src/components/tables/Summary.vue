<template>
  <form @input="total(); $emit('actualizado')">
    <button @click="serializar = !serializar">Serializar</button>
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
        <td>
          <input v-if="!serializar" type="text" v-model="data[f]">
          <span v-if="serializar">{{ data[f] }}</span>
        </td>
        <td>
          <span v-if="actual != null">{{ actual.minutos[f] }}</span>
        </td>
        <td>
          <span v-if="toDate == null">{{ actual.minutos[f] }}</span>
          <span v-if="toDate != null">{{ parseInt(toDate.minutos[f]) + parseInt(actual.minutos[f]) }}</span>
        </td>
      </tr>
      <tr>
        <th>Total</th>
        <td>{{ suma.plan }}</td>
        <td>{{ suma.actual }}</td>
        <td>{{ suma.toDate }}</td>
      </tr>
      </tbody>
    </table>
  </form>
</template>

<script>
  export default {
    props: ['titulo', 'data', 'actual', 'toDate', 'suma'],
    data() {
      return {
        serializar: false,
        filas: ['planning', 'design', 'code', 'compile', 'test', 'postmortem'],
        columnas: ['planned', 'actual', 'to date'],
      }
    },
    created() {
      console.log(this.data);
    },
    methods: {
      total: function () {
        this.suma.plan = 0;
        this.suma.actual = 0;
        this.suma.toDate = 0;
        Object.keys(this.data).forEach(fila => {
            this.suma.plan += parseInt(this.data[fila]);
        });
        Object.keys(this.data).forEach(fila => {
          this.suma.actual += parseInt(this.actual.minutos[fila]);
        });
        Object.keys(this.data).forEach(fila => {
          this.suma.toDate += parseInt(this.actual.minutos[fila]) + parseInt(this.toDate.minutos[fila]);
        });
      }
    },
  }
</script>

<style scoped>

</style>
