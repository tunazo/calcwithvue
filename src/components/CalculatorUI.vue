<template>
  <div class="calculator">
    <div class="display">{{ result || 0 }}</div>
    <div class="btn" @click="reset">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" data-operator="/" @click="setOperator">÷</div>
    <div class="btn" data-num="7" @click="add">7</div>
    <div class="btn" data-num="8" @click="add">8</div>
    <div class="btn" data-num="9" @click="add">9</div>
    <div class="btn operator" data-operator="*" @click="setOperator">X</div>
    <div class="btn" data-num="4" @click="add">4</div>
    <div class="btn" data-num="5" @click="add">5</div>
    <div class="btn" data-num="6" @click="add">6</div>
    <div class="btn operator" data-operator="-" @click="setOperator">-</div>
    <div class="btn" data-num="1" @click="add">1</div>
    <div class="btn" data-num="2" @click="add">2</div>
    <div class="btn" data-num="3" @click="add">3</div>
    <div class="btn operator" data-operator="+" @click="setOperator">+</div>
    <div class="btn zero" data-num="0" @click="add">0</div>
    <div class="btn" @click="point">.</div>
    <div class="btn operator" @click="equal">=</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      result: "",
      operator: null,
      previousNumber: null,
    };
  },
  methods: {
    setOperator(e) {
      // this.operator = symbol;
      this.operator = e.target.dataset.operator;
      [this.result, this.previousNumber] = ["", this.result];
    },
    add(e) {
      if (
        (this.result.charAt(0) === "0" && this.result.charAt(1) !== ".") ||
        this.result.length >= 10
      )
        return;
      this.result = `${this.result}${e.target.dataset.num}`;
      // this.result = `${this.result}${num}`;
    },
    reset() {
      // this.result = "";
      // this.previousNumber = this.operator = null;
      [this.result, this.previousNumber, this.operator] = ["", null, null];
    },
    sign() {
      this.result =
        this.result.charAt(0) === "-"
          ? this.result.slice(1)
          : this.result === ""
          ? ""
          : `-${this.result}`;
    },
    point() {
      if (this.result.indexOf(".") === 1) return;
      this.result = `${this.result}.`;
    },
    percent() {
      this.result = `${parseFloat(this.result) / 100}`;
    },
    equal() {
      // console.log(this.previousNumber, this.operator, this.result);
      if (!this.previousNumber || !this.result) return;
      this.result = eval(
        `${this.previousNumber} ${this.operator} ${this.result}`
      );
      this.result = (
        Number.isInteger(this.result)
          ? this.result
          : parseFloat(this.result).toFixed(5)
      ).toString();
    },
  },
};
</script>

<style scoped>
.calculator {
  width: 350px;
  margin: 20px auto;
  display: grid;
  font-size: 40px;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  grid-column: 1/5;
  background-color: #333;
  color: white;
}

.btn {
  background-color: #eee;
  border: 1px solid #999;
}
.operator {
  background-color: orange;
  color: white;
}
.zero {
  grid-column: 1/3;
}
</style>
