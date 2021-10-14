<template>
  <div id="app">
    <input type="text" class="display" value="0">
    <div class="container">
      <button v-on:click="resetValue()" class="greyBtn grid-item grid-item1">AC</button>
      <button class="greyBtn grid-item grid-item2">+/-</button>
      <button class="greyBtn grid-item grid-item3">%</button>
      <button v-on:click="appendToDisplay('/')" class="orangeBtn grid-item grid-item4">/</button>
      <button v-on:click="appendToDisplay('7')" class="grid-item grid-item5">7</button>
      <button v-on:click="appendToDisplay('8')" class="grid-item grid-item6">8</button>
      <button v-on:click="appendToDisplay('9')" class="grid-item grid-item7">9</button>
      <button v-on:click="appendToDisplay('*')" class="orangeBtn grid-item grid-item8">*</button>
      <button v-on:click="appendToDisplay('4')" class="grid-item grid-item9">4</button>
      <button v-on:click="appendToDisplay('5')" class="grid-item grid-item10">5</button>
      <button v-on:click="appendToDisplay('6')" class="grid-item grid-item11">6</button>
      <button v-on:click="appendToDisplay('-')" class="orangeBtn grid-item grid-item12">-</button>
      <button v-on:click="appendToDisplay('1')" class="grid-item grid-item13">1</button>
      <button v-on:click="appendToDisplay('2')" class="grid-item grid-item14">2</button>
      <button v-on:click="appendToDisplay('3')" class="grid-item grid-item15">3</button>
      <button v-on:click="appendToDisplay('+')" class="orangeBtn grid-item grid-item16">+</button>
      <button v-on:click="appendToDisplay('0')" class="grid-item grid-item17">0</button>
      <button v-on:click="appendToDisplay(',')" class="grid-item grid-item18">,</button>
      <button class="orangeBtn grid-item grid-item19">=</button>
    </div>
    
  </div>
</template>



<script>
import $ from "jquery";

export default {
  name: "App",
  methods: {
    appendToDisplay(value) {
      const displayValue = $(".display").val();
      if (displayValue === "0") {
        $(".display").val(value);
        return;
      }
      $(".display").val(displayValue + value);
    },
    resetValue() {
      $(".display").val(0);
    },
  },
};
</script>

<style>
#app {
  max-width: 320px;
}

.container {
  margin: 5px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 80px;
  grid-gap: 2px;
}

.grid-item {
  border: 1px solid black;
  border-radius: 10px;
  text-align: center;
  line-height: 80px;
  vertical-align: middle;
}

.display {
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

