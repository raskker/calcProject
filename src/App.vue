<template>
    <div class="container">
      <div class="display">{{current || '0'}}</div>
      <div @click="resetValue()" class="greyBtn grid-item grid-item1">AC</div>
      <div class="greyBtn grid-item grid-item2">+/-</div>
      <div class="greyBtn grid-item grid-item3">%</div>
      <div @click="divide" class="orangeBtn grid-item grid-item4">/</div>
      <div @click="appendToDisplay('7')" class="grid-item grid-item5">7</div>
      <div @click="appendToDisplay('8')" class="grid-item grid-item6">8</div>
      <div @click="appendToDisplay('9')" class="grid-item grid-item7">9</div>
      <div @click="multi" class="orangeBtn grid-item grid-item8">*</div>
      <div @click="appendToDisplay('4')" class="grid-item grid-item9">4</div>
      <div @click="appendToDisplay('5')" class="grid-item grid-item10">5</div>
      <div @click="appendToDisplay('6')" class="grid-item grid-item11">6</div>
      <div @click="minus" class="orangeBtn grid-item grid-item12">-</div>
      <div @click="appendToDisplay('1')" class="grid-item grid-item13">1</div>
      <div @click="appendToDisplay('2')" class="grid-item grid-item14">2</div>
      <div @click="appendToDisplay('3')" class="grid-item grid-item15">3</div>
      <div @click="plus" class="orangeBtn grid-item grid-item16">+</div>
      <div @click="appendToDisplay('0')" class="grid-item grid-item17">0</div>
      <div @click="dot()" class="grid-item grid-item18">.</div>
      <div @click="equal()" class="orangeBtn grid-item grid-item19">=</div>
    </div>
</template>



<script>
export default {
  name: "App",
  data() {
    return {
      current: "",
      operator: null,
      previous: null,
      operatorClicked: false,
    };
  },
  methods: {
    appendToDisplay(value) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${value}`;
    },
    resetValue() {
      this.current = "";
    },
    calculateValue() {},
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.appendToDisplay(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    multi() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },
  },
};
</script>

<style>
.container {
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.grid-item {
  border: 1px solid black;
  text-align: center;
  line-height: 80px;
  vertical-align: middle;
}

.display {
  grid-column: 1 / 5;
  width: 100%;
  height: 100px;
  border: 1px solid black;
  border-radius: 20px;
  background-color: black;
  text-align: right;
  color: white;
}

.grid-item17 {
  grid-column: span 2;
}

.greyBtn {
  background-color: rgb(206, 203, 203);
}

.orangeBtn {
  background-color: orange;
}

* {
  box-sizing: border-box;
}
</style>

