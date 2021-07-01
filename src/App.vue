<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />

    <div>
      <Go />
      <input type="number" placeholder="op1" v-model.number="operand1" />
      <input type="number" placeholder="op2" v-model.number="operand2" />
      = {{ sum }}
    </div>
    <button @click="sum = operand1 + operand2">+</button>
    <button @click="sum = operand1 - operand2">-</button>
    <button @click="sum = operand1 * operand2">*</button>
    <button @click="sum = Math.trunc(operand1 / operand2)">/</button>
    <button @click="sum = Math.pow(operand1, operand2)">xⁿ</button>
  </div>
</template>

<script>
import Go from "./components/Go.vue";

export default {
  name: "App",
  components: {
    Go,
  },
  data: () => ({
    operand1: "",
    operand2: "",
    sum: 0,
  }),
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
button {
  padding: 3px 12px;
}
</style>
