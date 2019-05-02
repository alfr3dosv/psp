<template>
  <form>
    <button @click="serializar = !serializar">
      Serializar
    </button>
    <table border="1">
      <thead>
      <td v-for="c in columnas">
        {{ c }}
      </td>
      </thead>
      <tbody>
      <tr v-for="f in filas">
        <td>{{ project }}</td>
        <td>{{ f }}</td>
        <td>

          <input v-if="serializar" @input="actualizarTiempo(f)" v-model="data.fechaInicio[f]">
          <span v-if="!serializar">{{data.fechaInicio[f]}}</span>
          <!--<input type="text" v-model="planned['plan'][f]">-->
        </td>
        <td>
          <input v-if="serializar" @input="actualizarTiempo(f)" v-model="data.interruption[f]">
          <span v-if="!serializar">{{data.interruption[f]}}</span>
        </td>
        <td>
          <input v-if="serializar" @input="actualizarTiempo(f)" v-model="data.fechaFin[f]">
          <span v-if="!serializar">{{data.fechaFin[f]}}</span>
        </td>
        <td>
          <span>{{ data.minutos[f]}}</span>
        </td>
      </tr>
      <tr>
        <th>Total</th>
        <!--<td>{{suma['plan']}}</td>-->
        <!--<td>{{ suma['actual']}}</td>-->
      </tr>
      </tbody>
    </table>
  </form>
</template>

<script>
  export default {
    name: "InputTable",
    props: ['titulo', 'planned', 'toDate', 'suma', 'data', 'project'],
    data() {
      return {
        serializar: true,
        filas: ['planning', 'design', 'code', 'compile', 'test', 'postmortem'],
        columnas: ['project', 'phase', 'Start Date and Time', 'Int. Time', 'Stop Date and Time', 'Delta Time'],
      }
    },
    created() {
      console.log(this.data);
    },
    methods: {
      actualizarTiempo: function (f) {
        let inicio = this.obtenerMinutos(this.data.fechaInicio[f]);
        console.log(inicio);
        let fin = this.obtenerMinutos(this.data.fechaFin[f]);
        let interrupcion = parseInt(this.data.interruption[f]);
        console.log(fin);
        this.data.minutos[f] = (fin - inicio) - interrupcion;
      },
      obtenerMinutos: function (fecha) {
        if (fecha != null && fecha.split != null && fecha.split(' ').length > 1) {
          let tiempo = fecha.split(' ')[1];
          let horas = 0;
          let minutos = 0;
          if (tiempo.split(':').length > 1) {
            horas = tiempo.split(':')[0];
            minutos = parseInt(tiempo.split(':')[1])
          } else {
            horas = parseInt(tiempo);
          }
          return (horas * 60) + minutos;
        }
        return 0;
      },
      total: function () {
        this.suma['plan'] = 0;
        this.suma['to date'] = 0;
        Object.keys(this.planned).forEach(columna => {
          Object.keys(this.planned[columna]).forEach(fila => {
            // console.log(this.data[fila][columna])
            if (columna === 'to date') {
              if (this.toDate != null) {
                this.planned[columna][fila] = parseInt(this.planned['plan'][fila]) + parseInt(this.toDate['plan'][fila])
                this.suma[columna] += parseInt(this.actual[columna][fila]);
              } else {
                this.planned[columna][fila] = parseInt(this.planned['plan'][fila])
                this.suma[columna] += parseInt(this.planned[columna][fila])
              }
            } else {
              this.suma[columna] += parseInt(this.planned[columna][fila]);
              console.log(columna + ' ' + fila + parseInt(this.planned[columna][fila]))
            }
          });
        });
      }
    },
  }
</script>

<style scoped>

</style>
