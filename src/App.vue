<template>
    <div class="container">
      <div class="display">
        <div class="value">
          {{current || '0'}}
        </div> 
      </div>
      <div @click="resetValue" class="greyBtn grid-item grid-item1">AC</div>
      <div @click="sign" class="greyBtn grid-item grid-item2">+/-</div>
      <div @click="percent" class="greyBtn grid-item grid-item3">%</div>
      <div @click="divide" :class="{pressed: isDivideClicked}" class="divide orangeBtn grid-item grid-item4">/</div>
      <div @click="appendToDisplay('7')" class="whiteBtn grid-item grid-item5">7</div>
      <div @click="appendToDisplay('8')" class="whiteBtn grid-item grid-item6">8</div>
      <div @click="appendToDisplay('9')" class="whiteBtn grid-item grid-item7">9</div>
      <div @click="multi" :class="{pressed: isMultipleClicked}" class="multi orangeBtn grid-item grid-item8">x</div>
      <div @click="appendToDisplay('4')" class="whiteBtn grid-item grid-item9">4</div>
      <div @click="appendToDisplay('5')" class="whiteBtn grid-item grid-item10">5</div>
      <div @click="appendToDisplay('6')" class="whiteBtn grid-item grid-item11">6</div>
      <div @click="minus" :class="{pressed: isMinusClicked}" class="minus orangeBtn grid-item grid-item12">-</div>
      <div @click="appendToDisplay('1')" class="whiteBtn grid-item grid-item13">1</div>
      <div @click="appendToDisplay('2')" class="whiteBtn grid-item grid-item14">2</div>
      <div @click="appendToDisplay('3')" class="whiteBtn grid-item grid-item15">3</div>
      <div @click="plus" :class="{pressed: isPlusClicked}" class="plus orangeBtn grid-item grid-item16">+</div>
      <div @click="appendToDisplay('0')" class="whiteBtn grid-item grid-item17">0</div>
      <div @click="dot" class="whiteBtn grid-item grid-item18">.</div>
      <div @click="equal" class="orangeBtn grid-item grid-item19">=</div>
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
      isMinusClicked: false,
      isPlusClicked: false,
      isDivideClicked: false,
      isMultipleClicked: false,
    };
  },
  methods: {
    appendToDisplay(value) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${value}`;
      this.resetClickedValues();
    },
    resetValue() {
      this.current = "";
      this.previous = null;
      this.resetClickedValues();
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.appendToDisplay(".");
        this.resetClickedValues();
      }
    },
    sign() {
      if (this.current != "") {
        this.current =
          this.current.charAt(0) === "-"
            ? this.current.slice(1)
            : `-${this.current}`;
      } else {
        this.current = "-0";
      }
      this.resetClickedValues();
    },
    resetClickedValues() {
      this.isMinusClicked = false;
      this.isPlusClicked = false;
      this.isDivideClicked = false;
      this.isMultipleClicked = false;
    },
    setClickedOperator(value) {
      if (value === "multi") {
        this.isMultipleClicked = true;
        this.isMinusClicked = false;
        this.isPlusClicked = false;
        this.isDivideClicked = false;
      } else if (value === "plus") {
        this.isPlusClicked = true;
        this.isMinusClicked = false;
        this.isDivideClicked = false;
        this.isMultipleClicked = false;
      } else if (value === "minus") {
        this.isMinusClicked = true;
        this.isPlusClicked = false;
        this.isDivideClicked = false;
        this.isMultipleClicked = false;
      } else if (value === "divide") {
        this.isDivideClicked = true;
        this.isMinusClicked = false;
        this.isPlusClicked = false;
        this.isMultipleClicked = false;
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.equal();
      this.operator = (a, b) => a / b;
      this.setPrevious();
      this.setClickedOperator("divide");
    },
    minus() {
      this.equal();
      this.operator = (a, b) => a - b;
      this.setPrevious();
      this.setClickedOperator("minus");
    },
    plus() {
      this.equal();
      this.operator = (a, b) => a + b;
      this.setPrevious();
      this.setClickedOperator("plus");
    },
    multi() {
      this.equal();
      this.operator = (a, b) => a * b;
      this.setPrevious();
      this.setClickedOperator("multi");
    },
    equal() {
      if (this.operator != null && this.previous !== null) {
        this.current = `${this.operator(
          parseFloat(this.previous),
          parseFloat(this.current)
        )}`;
      }
      this.previous = null;
      this.resetClickedValues();
    },
    percent() {
      if (this.current != "") {
        this.current = parseFloat(this.current) / 100;
      }
      this.resetClickedValues();
    },
  },
};
</script>

<style>
* {
  font-family: "Roboto", sans-serif;
}

.pressed {
  background-color: white !important;
  color: orange !important;
}

.container {
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.value {
  margin-right: 5px;
}

.grid-item {
  border: 1px solid #999;
  text-align: center;
  line-height: 80px;
  vertical-align: middle;
}

.orangeBtn:hover {
  background-color: white !important;
  color: orange !important;
}

.display {
  grid-column: 1 / 5;
  width: 100%;
  height: 100px;
  border: 1px solid #333;
  background-color: #333;
  text-align: right;
  color: white;
  line-height: 100px;
}

.grid-item17 {
  grid-column: span 2;
}

.greyBtn {
  background-color: rgb(206, 203, 203);
}

.greyBtn:hover {
  background-color: rgb(139, 134, 134) !important;
}

.orangeBtn {
  color: white;
  background-color: orange;
}

.whiteBtn:hover {
  background-color: orange;
  color: white !important;
}

* {
  box-sizing: border-box;
}
</style>

