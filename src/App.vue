<template>
  <div id="app">
    <h1>Math Quiz App</h1>
    <OperatorQuiz @onBack="clearOperator" v-if="operator" :operator="operator" />
    <OperatorSelector v-if="!operator" @changeOperator="changeOperator" />
  </div>
</template>

<script>
import OperatorSelector from "./components/OperatorSelector.vue";
import OperatorQuiz from "./components/OperatorQuiz.vue";
export default {
  name: "app",
  data() {
    return {
      operator: null
    };
  },
  methods: {
    changeOperator(operator) {
      this.operator = operator;
    },
    clearOperator() {
      this.operator = null;
    }
  },
  components: { OperatorSelector, OperatorQuiz }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 24px;
}
button {
  margin-right: 10px;
  border-color: #000;
  border: 5px solid;
  width: 160px;
  height: 100px;
  font-size: 24px;
  margin-top: 10px;
  cursor: pointer;
}

button:hover{
  border-color: #10aeb2;
}

button p:hover{
  color: #10aeb2;
}

h1{
  color: #10aeb2;
}
</style>