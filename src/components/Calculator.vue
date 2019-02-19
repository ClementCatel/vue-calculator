<template>
    <div class="calculator">
      <div class="display">2+2</div>
      <div class="display result">4</div>

      <div class="btn mem">mc</div>
      <div class="btn mem">m+</div>
      <div class="btn mem">m-</div>
      <div class="btn mem">mr</div>

      <div class="btn operator">C</div>
      <div class="btn operator fas fa-divide"></div>
      <div class="btn operator fas fa-times"></div>
      <div class="btn operator fas fa-backspace"></div>

      <div class="btn">7</div>
      <div class="btn">8</div>
      <div class="btn">9</div>
      <div class="btn operator fas fa-minus"></div>

      <div class="btn">4</div>
      <div class="btn">5</div>
      <div class="btn">6</div>
      <div class="btn operator fas fa-plus"></div>

      <div class="btn">1</div>
      <div class="btn">2</div>
      <div class="btn">3</div>
      <div class="btn equals fas fa-equals"></div>

      <div class="btn">%</div>
      <div class="btn">0</div>
      <div class="btn">.</div>
    </div>
</template>

<script>
export default {
  
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
    background-color: rgb(251, 251, 251);
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
    border: 0.1px solid rgb(223, 223, 223, 0.25);
    display: flex;
    align-items: center;
    justify-content: center; 
  }

  .operator {
    background-color: #eee;
    color: rgb(0, 98, 255);
    font-size: 26px;
    font-weight: bold;
  }
</style>
