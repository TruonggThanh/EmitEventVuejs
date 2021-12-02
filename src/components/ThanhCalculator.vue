<template>
  <div id="wrapper">
    <div id="calculator">
      <div class="calculator">
        <div class="calculator-display">
          {{ resultString }}
        </div>
        <div class="calculator-keypad">
          <div class="input-keys">
            <div class="function-keys">
              <button class="calculator-key key-clear" @click="reset">AC</button
              ><button class="calculator-key key-sign" @click="toggleNegative">
                ±</button
              ><button class="calculator-key key-percent" @click="percentive()">%</button>
            </div>
            <div class="digit-keys">
              <button class="calculator-key key-0" @click="operatorAdd('0')">0</button
              ><button class="calculator-key key-dot" @click="operatorAdd('.')">●</button>
              <button
                v-for="key in 9"
                :key="key"
                class="calculator-key"
                :class="`key-${key}`"
                @click="operatorAdd(key.toString())"
              >
                {{ key }}
              </button>
            </div>
          </div>
          <div class="operator-keys">
            <button class="calculator-key key-divide" @click="operatorAdd('/')">
              ÷</button
            ><button
              class="calculator-key key-multiply"
              @click="operatorAdd('*')"
            >
              ×</button
            ><button
              class="calculator-key key-subtract"
              @click="operatorAdd('-')"
            >
              −</button
            ><button class="calculator-key key-add" @click="operatorAdd('+')">
              +</button
            ><button
              class="calculator-key key-equals"
              @click="calculate()"
            >
              =
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LamCalculator",
  data() {
    return {
      result: 0,
      operator: "",    
      canDot: {
        d1: true,
        d2: true,
      },
    };
  },
  computed: {
    resultString: function () {
      return this.operator ? this.operator : this.result;
    },
  },
  updated() {},
  filters: {
    calculatorFormat: function (value) {
      let format = value.toString().replaceAll("/", "÷");
      format = format.toString().replaceAll("*", "×");
      return format;
    },
  },
  methods: {
    reset() {
      this.result = 0;
      this.operator = "";
      this.canDot.d1 = true;
      this.canDot.d2 = true;
    },
    isOperator(value) {
      return ["+", "-", "*", "/"].includes(value);
    },
    isDigit(value) {
      return ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"].includes(value);
    },
    toggleNegative() {
      this.result *= -1;
    },
    operatorAdd(value) {
      if (
        this.isDigit(value) &&
        (this.operator === "" || this.operator === "0")
      ) {
        this.reset();
      }
      if (this.operator === "" && value === "." && this.result !== 0) return;
      if (this.operator === "" && this.result === 0) {
          if(this.isOperator(value)){
              this.operator = "0"
          }
          if( value === "."){
            this.operator = "0";
            this.canDot.d2 = true;
          }
      }
      if (value === "." && (!this.canDot.d1 || !this.canDot.d2)) {
        return;
      }
      if (value === ".") {
        this.canDot.d1 = false;
        this.canDot.d2 = false;
      }
      if (this.isOperator(value)) {
        this.canDot.d1 = true;
      }
      if (this.isDigit(value)) {
        this.canDot.d2 = true;
      }

      if (this.result !== 0) {
        this.operator = this.result.toString();
        this.result = 0;
      }
      if (
        this.isOperator(value) &&
        this.isOperator(
          this.operator.toString().charAt(this.operator.length - 1)
        )
      ) {
        this.operator = this.operator.slice(0, this.operator.length - 1);
      }
      this.operator += value;
    },
    percentive() {
      this.calculate();
      this.result *= 0.01;
    },
    calculate() {
      if (!this.operator) return;
      this.result = eval(this.operator);
      this.operator = "";
    },
  },
};
</script>

<style scoped>
button {
  display: block;
  background: none;
  border: none;
  padding: 0;
  font-family: inherit;
  user-select: none;
  cursor: pointer;
  outline: none;

  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}

button:active {
  box-shadow: inset 0px 0px 80px 0px rgba(0, 0, 0, 0.25);
}

#wrapper {
  height: 100vh;

  display: flex;
  align-items: center;
  justify-content: center;
}

#calculator {
  width: 320px;
  height: 520px;
  position: relative;
}

.calculator {
  width: 100%;
  height: 100%;
  background: black;

  display: flex;
  flex-direction: column;
}

#wrapper .calculator {
  box-shadow: 0px 0px 20px 0px #aaa;
}

.calculator-display {
  color: white;
  background: #1c191c;
  line-height: 130px;
  font-size: 3em;
  overflow: hidden;
  position: relative;
  flex: 1;
      display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    align-content: flex-start;
    justify-content: flex-end;
    flex-wrap: nowrap;
}

.auto-scaling-text {
  display: inline-block;
}

.calculator-display .auto-scaling-text {
  padding: 0 20px;
  position: absolute;
  right: 0;
  transform-origin: right;
}

.calculator-keypad {
  height: 400px;

  display: flex;
}

.calculator .input-keys {
  width: 240px;
}

.calculator .function-keys {
  display: flex;
}

.calculator .digit-keys {
  background: #e0e0e7;

  display: flex;
  flex-direction: row;
  flex-wrap: wrap-reverse;
}

.calculator-key {
  width: 80px;
  height: 80px;
  border-top: 1px solid #777;
  border-right: 1px solid #666;
  text-align: center;
  line-height: 80px;
}
.calculator .function-keys .calculator-key {
  font-size: 2em;
}
.calculator .function-keys .key-multiply {
  line-height: 50px;
}
.calculator .digit-keys .calculator-key {
  font-size: 2.25em;
}
.calculator .digit-keys .key-0 {
  width: 160px;
  text-align: left;
  padding-left: 32px;
}
.calculator .digit-keys .key-dot {
  padding-top: 1em;
  font-size: 0.75em;
}
.calculator .operator-keys .calculator-key {
  color: white;
  border-right: 0;
  font-size: 3em;
}

.calculator .function-keys {
  background: linear-gradient(
    to bottom,
    rgba(202, 202, 204, 1) 0%,
    rgba(196, 194, 204, 1) 100%
  );
}
.calculator .operator-keys {
  background: linear-gradient(
    to bottom,
    rgba(252, 156, 23, 1) 0%,
    rgba(247, 126, 27, 1) 100%
  );
}
</style>