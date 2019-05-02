<template>
  <div>
    <input v-model="texto" type="text" name="todo">
    <button @click="agregar">Agregar</button>
    <ul>
      <li v-for="(i, index) in lista">
        <strong>{{ i }}</strong> <span @click="eliminar(index)">Eliminar</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  methods: {
    agregar() {
      console.log(this.texto);
      this.lista.push(this.texto);
    },
    eliminar(index) {
      console.log('eliminando ..');
      this.lista.pop(index);
    }
  },
  data() {
    return {
      texto: '',
      lista: []
    }
  }
}
</script>

<style scoped>
  span {
    padding-left: 20px;
  }
</style>
