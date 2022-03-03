<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <hr />
    <div class="display">
      <input v-model.number="operand1" />
      <input v-model.number="operand2" />
    </div>
    <div class="keyboard">
      <button @click="result = operand1 + operand2">+</button>
      <button @click="result = operand1 - operand2">-</button>
      <button v-if="operand2 != 0" @click="divide(operand1, operand2)">
        /
      </button>
      <button v-else @click="result = 'На 0 делить нельзя'">/</button>
      <button @click="multiply(operand1, operand2)">*</button>
      <button
        v-if="operand1 == 0 && operand2 < 0"
        @click="result = '0 в отрицательную степень возводить нельзя'"
      >
        ^
      </button>
      <button v-else @click="exponentiation(operand1, operand2)">^</button>
      <button v-if="operand2 != 0" @click="integerDivide(operand1, operand2)">
        целочисленное деление
      </button>
      <button v-else @click="result = 'На 0 делить нельзя'">
        целочисленное деление
      </button>
    </div>
    <div>Результат: {{ result }}</div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      message: "Hello Vue",
      operand1: 0,
      operand2: 0,
      result: 0,
    };
  },
  methods: {
    divide(op1, op2) {
      this.result = op1 / op2;
    },
    multiply(op1, op2) {
      this.result = op1 * op2;
    },
    exponentiation(op1, op2) {
      this.result =
        this.operand1 +
        " в " +
        this.operand2 +
        " степени = " +
        Math.pow(op1, op2);
    },
    integerDivide(op1, op2) {
      this.result = Math.trunc(op1 / op2);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
