<template>
    <div class="calculator">
      <div class="display m">{{memoryClicked}}</div>
      <div class="display" >{{ current || '0' }}</div>

      <div @click="memoryClear" class="btn mem" tabindex="1">mc</div>
      <div @click="memoryAdd" class="btn mem" tabindex="2">m+</div>
      <div @click="memoryMinus" class="btn mem" tabindex="3">m-</div>
      <div @click="memoryResult" class="btn mem" tabindex="4">mr</div>

      <div @click="clear" class="btn function" tabindex="5">C</div>
      <!-- <div @click="divide" class="btn operator fas fa-divide" tabindex="6"></div>
      <div @click="times" class="btn operator fas fa-times" tabindex="7"></div> -->
      <div @click="divide" class="btn function operator" tabindex="6">÷</div>
      <div @click="times" class="btn function operator" tabindex="7">×</div>
      <div @click="backspace" class="btn function material-icons" tabindex="8">backspace</div>

      <div @click="append('7')" class="btn" tabindex="9">7</div>
      <div @click="append('8')" class="btn" tabindex="10">8</div>
      <div @click="append('9')" class="btn" tabindex="11">9</div>
      <!-- <div @click="minus" class="btn operator fas fa-minus" tabindex="12"></div> -->
      <div @click="minus" class="btn function operator" tabindex="12">−</div>

      <div @click="append('4')" class="btn" tabindex="13">4</div>
      <div @click="append('5')" class="btn" tabindex="14">5</div>
      <div @click="append('6')" class="btn" tabindex="15">6</div>
      <!-- <div @click="add" class="btn operator fas fa-plus" tabindex="16"></div> -->
      <div @click="add" class="btn function operator" tabindex="16">+</div>

      <div @click="append('1')" class="btn" tabindex="17">1</div>
      <div @click="append('2')" class="btn" tabindex="18">2</div>
      <div @click="append('3')" class="btn" tabindex="19">3</div>
      <!-- <div @click="equals" class="btn equals fas fa-equals" tabindex="20"></div> -->
      <div @click="equals" class="btn equals operator" tabindex="20">=</div>

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
      operator: null,
      operatorClicked: false,
      memoryClicked: '',
      memory : 0,
    }
  },
  methods: {
    clear() {
      this.current = '';
      this.operator = this.previous = null;
      this.operatorClicked = false;
    },

    memoryClear() {
      this.memory = 0;
      this.memoryClicked = '';
    },

    memoryAdd() {
      this.memory += parseFloat(this.current);
      this.memoryClicked = 'M';
    },

    memoryMinus() {
      this.memory -= parseFloat(this.current);
      this.memoryClicked = 'M';
    },

    memoryResult() {
      if (this.memoryClicked) {
        this.current = `${this.memory}`;
      }
    },

    backspace() {
      if (!this.operatorClicked) {
        this.current = this.current.slice(0, this.current.length - 1);
      }
    },

    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
 
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },

    dot() {
      if (!this.current.includes('.')) {
        this.current = `${this.current}${'.'}`
      }  
    },

    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },

    divide() {
      this.operator = (a, b) => a / b ;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b ;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b ;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b ;
      this.setPrevious();
    },

    equals() {
      if (this.operator) {
        this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.previous = null;
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator {
    margin: 0 auto;
    width: 320px;
    font-size: 30px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(80px, auto);
    background-color: white;
  }

  .display {
    grid-column: 1 / 5;
    font-size: 42px;
    display: flex;
    align-items: center;
    margin-left: auto;
    margin-right: 5%;
  }

  .m {
    font-size: 16px;
    color: #888;
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

  .function {
    background-color: #eee;
    color: rgb(0, 98, 255);
    font-size: 26px;
  }

  .operator {
    font-family: 'Roboto', sans-serif;
    font-weight: 300;
    font-size: 40px;
  }

</style>
