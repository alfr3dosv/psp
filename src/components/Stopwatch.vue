<template>
  <div>
    <h1>Time</h1>
    <button @click="contar('planning')">Planning</button>
    <button @click="contar('design')">Design</button>
    <button @click="contar('code')">Code</button>
    <button @click="contar('compile')">Compile</button>
    <button @click="contar('test')">Test</button>
    <button @click="contar('postmortem')">Postmortem</button>
    <br>
    <div v-if="parte != ''">
      <h1>{{parte}}</h1>
    </div>
    <div v-if="parte != ''">
      <button @click="parte = ''">Pausar</button>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Stopwatch",
    mounted() {
      setInterval(this.updateCurrentTime, 1000);
      console.log('mounted')
    },
    methods: {
      updateCurrentTime(t) {
        if (this.tiempos[this.parte] == null)
          this.tiempos[this.parte] = 0;
        this.tiempos[this.parte] += 1;
        console.log(this.tiempos[this.parte]);
      },
      contar(parte) {
        this.parte = parte;
      }
    },
    data() {
      return {
        time: 0,
        parte: 'planning',
        tiempos: {}
      }
    }
  }
</script>

<style scoped>

</style>
