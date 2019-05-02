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
          <span v-if="toDate != null">{{ parseInt(getToDate().minutos[f]) }}</span>
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
      getToDate() {
        let suma = {minutos: {}};
        this.toDate.forEach(d => {
           Object.keys(d.minutos).forEach(k => {
             // console.log(k);
             if (suma.minutos[k] == null)
              suma.minutos[k] = 0;
             suma.minutos[k] += d.minutos[k] + this.actual.minutos[k];
           });
        });
        // Object.keys(this.toDate.minutos).forEach(k => {
        //   console.log(k);
        //   for (let i = 0; i < this.toDate.length; i++) {
        //     console.log(k);
        //     if (suma.minutos[k] == null)
        //       suma.minutos[k] = 0;
        //     console.log(suma.minutos[k]);
        //     suma.minutos[k] += this.toDate[i].minutos[k];
        //   }
        // });
        return suma;
      },
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
        console.log('to date')
        let toDate = this.getToDate();
        console.log(toDate);
        Object.keys(toDate.minutos).forEach(fila => {
          console.log(fila);
          this.suma.toDate += parseInt(toDate.minutos[fila]);
        });
      }
    },
  }
</script>

<style scoped>

</style>
