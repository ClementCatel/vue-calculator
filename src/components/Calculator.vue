<template>
    <div class="calculator">
      <div class="display" >{{ current || '0' }}</div>
      <div class="display result">{{ result }}</div>

      <div class="btn mem" tabindex="1">mc</div>
      <div class="btn mem" tabindex="2">m+</div>
      <div class="btn mem" tabindex="3">m-</div>
      <div class="btn mem" tabindex="4">mr</div>

      <div @click="clear" class="btn operator" tabindex="5">C</div>
      <div @click="divide" class="btn operator fas fa-divide" tabindex="6"></div>
      <div @click="times" class="btn operator fas fa-times" tabindex="7"></div>
      <div @click="backspace" class="btn operator fas fa-backspace" tabindex="8"></div>

      <div @click="append('7')" class="btn" tabindex="9">7</div>
      <div @click="append('8')" class="btn" tabindex="10">8</div>
      <div @click="append('9')" class="btn" tabindex="11">9</div>
      <div @click="minus" class="btn operator fas fa-minus" tabindex="12"></div>

      <div @click="append('4')" class="btn" tabindex="13">4</div>
      <div @click="append('5')" class="btn" tabindex="14">5</div>
      <div @click="append('6')" class="btn" tabindex="15">6</div>
      <div @click="add" class="btn operator fas fa-plus" tabindex="16"></div>

      <div @click="append('1')" class="btn" tabindex="17">1</div>
      <div @click="append('2')" class="btn" tabindex="18">2</div>
      <div @click="append('3')" class="btn" tabindex="19">3</div>
      <div @click="equals" class="btn equals fas fa-equals" tabindex="20"></div>

      <div @click="percent" class="btn" tabindex="21">%</div>
      <div @click="append('0')" class="btn" tabindex="22">0</div>
      <div @click="dot" class="btn" tabindex="23">.</div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      currentValue: '',
      result: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = this.result = this.currentValue = '';
      this.operator = this.previous = null;
    },

    backspace() {
      this.current = this.current.slice(0, this.current.length - 1);
      this.compute();
      this.operatorClicked = false;
    },

    compute() {
      if (this.operator != null) {
        this.result = `${this.operator(parseFloat(this.previous), parseFloat(this.currentValue))}`;
      }
    },

    // TODO : recalculate the percentage every time it is clicked
    percent() {
      this.current = `${this.current}${'%'}`;
      this.result = `${parseFloat(this.current) / 100}`;
    },
 
    append(number) {
      this.current = `${this.current}${number}`;
      this.currentValue = `${this.currentValue}${number}`;
      this.compute();
      this.operatorClicked = false;
    },

    appendOperator(operator) {
      if (this.current !== '' && !this.operatorClicked) {
        this.current = `${this.current}${operator}`;
      }
    },

    dot() {
      if (!this.current.includes('.')) {
        this.current = `${this.current}${'.'}`
      }  
    },

    setPrevious() {
      this.result === '' ?
        this.previous = this.currentValue : this.previous = this.result;
      this.currentValue = '';
      this.operatorClicked = true;
    },

    divide() {
      this.operator = (a, b) => a / b;
      this.appendOperator('÷')
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.appendOperator('×')
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.appendOperator('−')
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.appendOperator('+')
      this.setPrevious();
    },

    equals() {
      this.current = this.currentValue = this.result;
      this.result = '';
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator {
    margin: 0 auto;
    width: 400px;
    font-size: 30px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(100px, auto);
    background-color: white;
  }

  .display {
    grid-column: 1 / 5;
    font-size: 48px;
    display: flex;
    align-items: center;
    margin-left: auto;
    margin-right: 5%;
  }

  .result {
    color: #888;
    font-size: 30px;
  }

  .mem {
    background-color: #eee;
    color: #888
  }

  .equals {
    grid-column: 4 / 5;
    grid-row: 7 / 9;
    background-color: rgb(0, 98, 255);
    color: white;
    font-size: 26px;
  }

  .btn {
    border: 1px solid rgb(223, 223, 223, 0.25);
    display: flex;
    align-items: center;
    justify-content: center; 
  }

  .btn :focus {
    background-color: #aaa
  }

  .operator {
    background-color: #eee;
    color: rgb(0, 98, 255);
    font-size: 26px;
    font-weight: bold;
  }
</style>
