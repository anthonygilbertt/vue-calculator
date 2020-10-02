<template>
  <div class="calculator"><h1>Vue.js Calculator</h1>
   <button class="display">{{ current || 0 }}</button>
   <button @click="clear" class="btn">C</button>
   <button @click="sign"  class="btn">+/-</button>
   <button @click="percent" class="btn">%</button>
   <button @click="divide" class="btn operator">÷</button>
   <button @click="append('7')" class="btn">7</button>
   <button @click="append('8')" class="btn">8</button>
   <button @click="append('9')" class="btn">9</button>
   <button @click="times" class="btn operator">X</button>
   <button @click="append('4')" class="btn">4</button>
   <button @click="append('5')" class="btn">5</button>
   <button @click="append('6')" class="btn">6</button>
   <button @click="minus" class="btn operator">-</button>
   <button @click="append('1')" class="btn">1</button>
   <button @click="append('2')" class="btn">2</button>
   <button @click="append('3')" class="btn">3</button>
   <button @click="add" class="btn operator">+</button>
   <button @click="append('0')" class="zero btn">0</button>
   <button @click="dot" class="btn">.</button>
   <button @click="equals" class="btn operator">=</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false
      }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      if (this.current === `-0` || `-`) {
      this.current = 0;
      } else if  (this.current < 0 ) {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) :   `-${this.current}`;  
      }
      else {  
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) :   `-${this.current}`;
      }
      // if (this.current === '-') {
      // this.current === 0;
    },
    percent() {
      this.current = this.current / 100;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      // this.current = this.current + '/';
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    minus() {
      // this.current = this.current + '-';
      this.operator = (a, b) => a - b;
      this.setPrevious();
      if (this.current === this.current) {
        return this.current;
      }
    },
    times() {
      // this.current = this.current + '*';
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    add() {
      // this.current = this.current + '+';
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equals() {
      if (this.current === this.current) {
        this.current;
      } else {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
      }
    },
  }
}


/* Future Improvements
-------------------------
1)  fix */
</script>

<style scoped>
h1 {
  grid-column: 1/5;
  margin-top: -30px!important;
}
.zero{
grid-column: 1/3;
}
.display {
 display: grid;
 grid-column: 1/5;
 background-color:#333;
 color:white;
 align-items:center;
 padding: 10px 10px 10px 10px ;
}
.calculator{
 display: grid;
 grid-template-columns: repeat(4, 1fr);
 grid-auto-rows: minmax(50px, auto);
  align-items:center;
 }
 .btn {
 background-color: #eee;
 border:1px solid #999;
 margin: 0px 5px 5px 5px;
 padding: 10px 10px 10px 10px;
 }
 .btn:hover {
   border: 1px solid black;
 margin: 0px 5px 5px 5px;
 padding: 10px 10px 10px 10px;
 }
 .operator {
 background-color: orange;
 color: white;
 }

</style>
