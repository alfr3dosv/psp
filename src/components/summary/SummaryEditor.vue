<template>
  <div class="main">
    <form @input="update">
      <div>
        <button @click="mostrarActual=!mostrarActual">
          <span v-if="mostrarActual">Editar Plan</span>
          <span v-if="!mostrarActual">Editar Actual</span>
        </button>
        <button @click="mostrarPrevio=!mostrarPrevio">
          <span v-if="!mostrarPrevio">Mostrar previo</span>
          <span v-if="mostrarPrevio">Ocultar previo</span>
        </button>
      </div>
      <table>
        <thead>
        <tr>
          <th>Summary</th>
          <th v-if="!mostrarActual">Plan</th>
          <th v-if="mostrarActual">Actual</th>
        </tr>
        </thead>
        <tbody>
        <tr>
          <th>Program size</th>
          <th v-if="!mostrarActual">Plan</th>
          <th v-if="mostrarActual">Actual</th>
        </tr>
        <tr>
          <td>Base(B)</td>
          <td v-if="!mostrarActual"><input v-model="summary.base.plan"></td>
          <td v-if="mostrarActual"><input v-model="summary.base.actual"></td>
        </tr>
        <tr>
          <td>Deleted(D)</td>
          <td v-if="!mostrarActual"><input v-model="summary.deleted.plan"></td>
          <td v-if="mostrarActual"><input v-model="summary.deleted.actual"></td>
        </tr>
        <tr>
          <td>Modified(M)</td>
          <td v-if="!mostrarActual"><input v-model="summary.modified.plan"></td>
          <td v-if="mostrarActual"><input v-model="summary.modified.actual"></td>
        </tr>
        <tr>
          <td>Added(A)</td>
          <td v-if="!mostrarActual"><input v-model="summary.added.plan"></td>
          <td v-if="mostrarActual"><input v-model="summary.added.actual"></td>
        </tr>
        <tr>
          <td>Reused(R)</td>
          <td v-if="!mostrarActual"><input v-model="summary.reused.plan"></td>
          <td v-if="mostrarActual"><input v-model="summary.reused.actual"></td>
        </tr>
        <tr>
          <td>Added and Modified (A+M)</td>
          <td v-if="!mostrarActual"><input v-model="summary.addedAndModified.plan"></td>
          <td v-if="mostrarActual"><input v-model="summary.addedAndModified.actual"></td>
        </tr>
        <tr>
          <td>Total Size(T)</td>
          <td v-if="!mostrarActual">{{ summary.totalSize.plan }}</td>
          <td v-if="mostrarActual">{{ summary.totalSize.actual }}</td>
        </tr>
        <tr>
          <td>Total New Reusable</td>
          <td>4</td>
          <td v-if="mostrarActual">4</td>
        </tr>
        <tr>
          Estimated Proxy Size (E)
        </tr>
        </tbody>
      </table>
    </form>
    <div v-if="mostrarPrevio">
      <SummaryPrint :summary="summary"></SummaryPrint>
    </div>
  </div>
</template>

<script>
  import SummaryPrint from './SummaryPrint';
  export default {
    name: "SummaryEditor",
    components: {SummaryPrint},
    methods: {
      update() {
        console.log('cambio')
      }
    },
    data() {
      return {
        mostrarActual: false,
        mostrarPrevio: false,
        summary: {
          base: {
            plan: 0,
            actual: 0
          },
          deleted: {
            plan: 0,
            actual: 0,
          },
          modified: {
            plan: 0,
            actual: 0,
          },
          added: {
            plan: 0,
            actual: 0
          },
          reused: {
            plan: 0,
            actual: 0
          },
          addedAndModified: {
            plan: 0,
            actual: 0
          },
          totalSize: {
            plan: 0,
            actual: 0
          },
          totalNewReusable: {
            plan: 0,
            actual: 0
          }
        }
      }
    }
  }
</script>

<style scoped>
.main {
  display: flex;
}
</style>
