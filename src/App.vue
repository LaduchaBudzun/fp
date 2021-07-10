<template>
  <div id="app">
    <marquee behavior="operand2" direction="operand2"></marquee>
    <img alt="Vue logo" src="./assets/logo.png" />

    <div>
      <Go />
      <input type="number" placeholder="op1" v-model.number="operand1" />
      <input type="number" placeholder="op2" v-model.number="operand2" />
      = {{ result }} - {{ fibResult }}
    </div>
    <div class="error" v-if="error">Ошибка: {{ error }}</div>

    <div class="strange-message">
      <template v-if="result < 0">Отрицательное число</template>
      <template v-else-if="result < 100">Число меньше 100 </template>
      <template v-else>Число больше 100</template>
    </div>

    <div class="buttons">
      <button
        v-for="btn in buttons"
        :key="btn"
        @click="calculate(btn)"
        :disabled="operand2 === 0"
      >
        {{ btn }}
      </button>

      <div class="checkbox">
        <input type="checkbox" checked v-model="checked" />Отобразить экранную
        клавиатуру
      </div>

      <div class="keyboard" v-if="checked">
        <div class="numbers">
          <button v-for="num in collection" :key="num" @click="numbers(num)">
            {{ num }}
          </button>
        </div>
        <div class="radio">
          <div class="radio-child">
            <input type="radio" id="one" value="1" v-model="picked" checked />
            <label for="one">Операнд 1</label>
          </div>
          <div class="radio-child">
            <input type="radio" id="two" value="2" v-model="picked" />
            <label for="two">Операнд 2</label>
          </div>
        </div>
      </div>
    </div>
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
    result: 0,
    fibResult: 0,
    error: "",
    buttons: ["+", "-", "*", "/", "**"],
    collection: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
    num: 0,
    checked: true,
    picked: "",
  }),
  methods: {
    numbers(number) {
      if (this.picked == 1) {
        this.operand1 = this.operand1.toString() + number.toString();
        this.operand1 = Number(this.operand1);
      } else if (this.picked == 2) {
        this.operand2 = this.operand2.toString() + number.toString();
        this.operand2 = Number(this.operand2);
      }
    },

    fib(n) {
      return n <= 1 ? n : this.fib(n - 1) + this.fib(n - 2);
    },

    calculate(operation = "+") {
      this.error = ""; //обновляем ошибку
      switch (operation) {
        case "+":
          this.add();
          break;
        case "-":
          this.sub();
          break;
        case "*":
          this.mul();
          break;
        case "/":
          this.divis();
          break;
        case "**":
          this.exp();
          break;
      }
      const key = Date.now();
      const value = `${this.operand1} ${operation} ${this.operand2} = ${this.result}`;
      this.$set(this.logs, key, value); //реактивность объекта
    },
    add() {
      this.result = this.operand1 + this.operand2;
      // this.fibResult = this.fib(this.operand1) + this.fib(this.operand2);
      this.fibResult = this.fib1 + this.fib2;
    },
    sub() {
      this.result = this.operand1 - this.operand2;
      this.fibResult = this.fib1 - this.fib2;
    },
    mul() {
      this.result = this.operand1 * this.operand2;
    },
    divis() {
      const { operand1, operand2 } = this;
      if (operand2 === 0) {
        this.error = "На 0 делить нельзя!";
      } else {
        this.result = Math.trunc(operand1 / operand2);
      }
    },
    exp() {
      this.result = Math.pow(this.operand1, this.operand2);
    },
  },
  computed: {
    fib1() {
      return this.fib(this.operand1);
    },
    fib2() {
      return this.fib(this.operand2);
    },
  },
};
</script>

<style scoped>
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
  margin: 3px;
}
.error {
  color: red;
}
.checkbox {
  margin-top: 50px;
  margin-bottom: 20px;
}
.radio {
  margin-top: 15px;
  display: flex;
  justify-content: center;
}
.radio-child {
  display: flex;
}

.radio-child:last-child {
  margin-left: 30px;
}
</style>
