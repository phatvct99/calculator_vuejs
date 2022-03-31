<template>
  <div class="calculator">
    <div class="display">{{ current || '0'}}</div>
    <div class = "btn operator">MC</div>
    <div class = "btn operator">MR</div>
    <div class = "btn operator">M+</div>
    <div class = "btn operator">M-</div>
    <div @click="clear" class = "btn danger">CE</div>
    <div @click="append('7')" class = "btn">7</div>
    <div @click="append('8')" class = "btn">8</div>
    <div @click="append('9')" class = "btn">9</div>
    <div @click="divide" class = "btn operator">/</div>
    <div class = "btn operator">√</div>
    <div @click="append('4')" class = "btn">4</div>
    <div @click="append('5')" class = "btn">5</div>
    <div @click="append('6')" class = "btn">6</div>
    <div @click="times" class = "btn operator">x</div>
    <div @class="percent" class = "btn operator">%</div>
    <div @click="append('1')" class = "btn">1</div>
    <div @click="append('2')" class = "btn">2</div>
    <div @click="append('3')" class = "btn">3</div>
    <div @click="minus" class = "btn operator">-</div>
    <div class = "btn operator">1/x</div>
    <div @click="append('0')" class = "btn">0</div>
    <div @click="dot" class = "btn">.</div>
    <div @click="sign" class = "btn">+/-</div>
    <div @click="add" class = "btn operator">+</div>
    <div @click="equal" class = "btn operator">=</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      current: '',
      operator: null,
      previous: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear () {
      this.current = ''
    },
    sign () {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
    },
    append (number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`
    },
    dot() {
      if (this.current.indexOf('.') === -1 ) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked =true;
    },
    divide() {
      this.operator = (a, b) => a/b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a*b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a-b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a+b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
        )}`;
        this.previous = null;
    },
    percent () {
      this.current = `${parseFloat(this.current) / 100}`;
    },
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator{
  width: 300px;
  height: 400px;
  margin: auto;
  font-size: 20px;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-auto-rows: minmax(50px, auto);
  border-radius: 15px 15px 1px 1px;
  border: 6px solid #333;
  padding: 3px;
 
  
}
.display{
  grid-column: 1/6;
  background: rgb(217, 241, 225);
  color: #000;
  border: 1px solid #000;
  border-radius: 5px;
  font-weight: bold;
  margin-bottom: 10px;
}
.btn{
  background-color: #fff;
  border: 1px solid rgb(192, 190, 190);
  border-radius: 5px;
  margin: 2px;
  text-align: center;
  font-weight: bold;
  padding-top:20px;
}
.operator{
background-color: rgb(108, 250, 132);
}
.danger{
  background-color: rgb(248, 129, 108);
}
a {
  color: #42b983;
}
</style>
