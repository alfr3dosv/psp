<template>
  <div id="app">
    <div>
      <button @click="seleccionado = 1">Trabajo 1</button>
      <button @click="seleccionado = 2">Trabajo 2</button>
      <button @click="seleccionado = 3">Trabajo 3</button>
    </div>
    <br>
    <div :class="seleccionado !== 1 ? 'd-none':''">
      <TimeTable project="2" :data="trabajo1.time">

      </TimeTable>
      <br>
      <Summary titulo="Summary time" :data="trabajo1.summary"
               :actual="trabajo1.time"
               :suma="trabajo1.suma.summary">
      </Summary>
      <br>
      <DefectsTable titulo="Defects injected 1" :actual="trabajo1.defectos"
                    :suma="trabajo1.suma.defectos">
      </DefectsTable>
    </div>
    <div :class="seleccionado !== 2 ? 'd-none':''">
      <TimeTable project="2" :data="trabajo2.time">

      </TimeTable>
      <br>
      <Summary titulo="Summary time 2" :data="trabajo2.summary"
               :to-date="trabajo1.time"
               :actual="trabajo2.time"
               :suma="trabajo2.suma.summary">
      </Summary>
      <br>
      <DefectsTable titulo="Defects injected 2" :actual="trabajo2.defectos"
                    :suma="trabajo2.suma.defectos"
                    :to-date="trabajo1.defectos"
      >
      </DefectsTable>
    </div>
    <div :class="seleccionado !== 3 ? 'd-none':''">
      <TimeTable project="2" :data="trabajo3.time">

      </TimeTable>
      <br>
      <Summary titulo="Summary time 3" :data="trabajo3.summary"
               :to-date="sumarTime(trabajo1.time, trabajo2.time"
               :actual="trabajo3.time"
               :suma="trabajo3.suma.summary">
      </Summary>
      <br>
      <DefectsTable titulo="Defects injected 3" :actual="trabajo3.defectos"
                    :suma="trabajo3.suma.defectos"
                    :to-date="trabajo3.defectos"
      >
      </DefectsTable>
    </div>
  </div>
</template>

<script>
  import Summary from './components/tables/Summary';
  import DefectsTable from './components/tables/DefectsTable';
  import TimeTable from './components/tables/TimeTable';

  export default {
    name: 'App',
    components: {
      DefectsTable, Summary, TimeTable
    },
    data() {
      return {
        seleccionado: 1,
        trabajo1: {
          defectos: {}, summary: {}, time: {},
          suma: {defectos: {actual: 0, toDate: 0}, summary: {actual: 0, toDate: 0}}
        },
        trabajo2: {
          defectos: {}, summary: {}, time: {},
          suma: {defectos: {actual: 0, toDate: 0}, summary: {actual: 0, toDate: 0}}
        },
        trabajo3: {
          defectos: {}, summary: {}, time: {},
          suma: {defectos: {actual: 0, toDate: 0}, summary: {actual: 0, plan: 0, toDate: 0}}
        }
      }
    },
    methods: {
      defectsData() {
        return {'planning': 0, 'design': 0, 'code': 0, 'compile': 0, 'test': 0};
        // 'to date': {'planning': 0, 'design': 0, 'code': 0, 'compile': 0, 'test': 0},
        // };
      },
      timeData() {
        return {
          fechaInicio: {'planning': 0, 'design': 0, 'code': 0, 'compile': 0, 'test': 0, 'postmortem': 0},
          fechaFin: {'planning': 0, 'design': 0, 'code': 0, 'compile': 0, 'test': 0, 'postmortem': 0},
          interruption: {'planning': 0, 'design': 0, 'code': 0, 'compile': 0, 'test': 0, 'postmortem': 0},
          minutos: {'planning': 0, 'design': 0, 'code': 0, 'compile': 0, 'test': 0, 'postmortem': 0},
        }
      },
      summaryData() {
        return {'planning': 0, 'design': 0, 'code': 0, 'compile': 0, 'test': 0, 'postmortem': 0}
      },
      sumarDefectos(d1, d2) {
        suma = {};
        Object.keys(d1).forEach(k => {
          for (i = 0; i < arguments.length; i++) {
            suma[k] += arguments[i][k]
          }
        })
      },
      sumarTime(d1, d2) {
        suma = {minutos: {}};
        Object.keys(d1).forEach(k => {
          for (i = 0; i < arguments.length; i++) {
            suma.minutos[k]
            suma.minutos[k] += d1.minutos[k] + d2.minutos[k];
          }
        })
      }
    },
    created() {
      this.trabajo1.defectos = this.defectsData();
      this.trabajo1.summary = this.summaryData();
      this.trabajo1.time = this.timeData();
      this.trabajo2.defectos = this.defectsData();
      this.trabajo2.summary = this.summaryData();
      this.trabajo2.time = this.timeData();
      this.trabajo3.defectos = this.defectsData();
      this.trabajo3.summay = this.summaryData();
      this.trabajo3.time = this.timeData();
    }
  }

</script>

<style>
</style>
