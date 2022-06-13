<template>
  <div id="app">
    <h1>Math Quiz App</h1>
    <OperatorQuiz @onBack="clearOperator" v-if="operator" :operator="operator" />
    <OperatorSelector v-if="!operator" @changeOperator="changeOperator" />
  </div>
</template>

<script>
import OperatorSelector from './components/OperatorSelector.vue';
import OperatorQuiz from './components/OperatorQuiz.vue';
export default {
  name: 'App',
  data() {
    return {
      operator: null
    }
  },
  methods: {
    changeOperator(operator) {
      this.operator = operator;
    },
    clearOperator() {
      this.operator = null;
    },
  },
  components: {
    OperatorSelector,
    OperatorQuiz
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 24px;
}

button {
  margin: 10px;
  padding: 15px;
  width: 160px;
  margin-right: 15px;
  height: 80px;
  background-color: #12d418;
  color: #FFF;
  font-size: 24px;
  cursor: pointer;
  vertical-align: top;
}
</style>
