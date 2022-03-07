<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <hr />
    <div class="display">
      <input v-model.number="showOperand1" />
      <input v-model.number="showOperand2" />
    </div>
    <div class="keyboard">
      <button @click="result = showOperand1 + showOperand2">+</button>
      <button @click="result = showOperand1 - showOperand2">-</button>
      <button v-if="operand2 != 0" @click="divide(showOperand1, showOperand2)">
        /
      </button>
      <button v-else @click="result = 'На 0 делить нельзя'">/</button>
      <button @click="multiply(showOperand1, showOperand2)">*</button>
      <button
        v-if="showOperand1 == 0 && showOperand2 < 0"
        @click="result = '0 в отрицательную степень возводить нельзя'"
      >
        ^
      </button>
      <button v-else @click="exponentiation(showOperand1, showOperand2)">
        ^
      </button>
      <button
        v-if="showOperand2 != 0"
        @click="integerDivide(showOperand1, showOperand2)"
      >
        целочисленное деление
      </button>
      <button v-else @click="result = 'На 0 делить нельзя'">
        целочисленное деление
      </button>
    </div>
    <div>Результат: {{ result }}</div>
    <label
      ><input type="checkbox" v-model="show" />Отобразить экранную
      клавиатуру</label
    >
    <div class="btns__number" v-show="show">
      <button
        v-for="number of numbers"
        :key="number"
        @click="writeNumber(number)"
      >
        {{ number }}
      </button>
    </div>
    <div>
      <label
        ><input
          type="radio"
          value="operand1"
          v-model="operand"
          name="operand"
        />
        Операнд 1</label
      >
      <label
        ><input
          type="radio"
          value="operand2"
          v-model="operand"
          name="operand"
          checked
        />
        Операнд 2</label
      >
    </div>
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
      operand1: [],
      operand2: [],
      result: 0,
      show: true,
      operand: "operand1",
      numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, "удалить"],
    };
  },
  computed: {
    showOperand1() {
      return +this.operand1.join("");
    },
    showOperand2() {
      return +this.operand2.join("");
    },
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
        this.showOperand1 +
        " в " +
        this.showOperand2 +
        " степени = " +
        +Math.pow(op1, op2);
    },
    integerDivide(op1, op2) {
      this.result = Math.trunc(op1 / op2);
    },
    writeNumber(number) {
      if (this.operand == "operand1") {
        if (number == "удалить") {
          this.operand1.pop();
        } else {
          this.operand1.push(number);
        }
      } else if (this.operand == "operand2") {
        if (number == "удалить") {
          this.operand2.pop();
        } else {
          this.operand2.push(number);
        }
      }
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
