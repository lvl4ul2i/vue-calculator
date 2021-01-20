<template>
  <div class="calculator" :class="{ onDragging: dragStart}">
    <div class="display">{{current ||  '0'}}</div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="divide">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="times">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="minus">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="add">+</div>
    <div class="btn cero" @click="append('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="equal">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  props:{
    dragStart:{
      type: Boolean,
      required: true
    }
  },
  data(){
    return{
      current:"0",
      operator: null,
      previuos: null,
      operatorClicked: false,
    }
  },
  methods:{
    append(num){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${num}`;
    },
    clear(){
      this.current = '';
    },
    sign(){
      this.current = this.current.charAt(0) === '-' 
      ? this.current.slice(1)
      : `-${this.current}`;
    },
    percent(){
      this.current = `${parseFloat(this.current) / 100}`;
    },
    dot(){
      if(this.current.indexOf('.') === -1 && this.current != ''){
        this.append('.')
      }
      else if(this.current.indexOf('.') === -1 && this.current === ''){
        this.append('0.')
      }
    },
    setPrevious(){
      this.previuos = this.current;
      this.operatorClicked = true;
    },
    divide(){
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times(){
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus(){
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add(){ 
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal(){
      this.current = `${this.operator(parseFloat(this.previuos),parseFloat(this.current))}`;
      this.previuos = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator{
    width: 145px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(30px, auto);
}
.display{
    cursor: move;
    cursor: grab;
    cursor: -moz-grab;
    cursor: -webkit-grab;
    font-size: 30px;
    grid-column: 1 / 5;
    background-color: #4c4c4c;
    color: #fff;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    padding: 15px 10px 0px;
}
.cero{
  grid-column: 1 / 3;
}
.btn{
    display: flex;
    font-size: 16px;
    font-weight: 500;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    background-color: #e0e0e0;
    border: 1px solid #8e8e8e;
}
.btn:active {
   transform: scale(0.95);
}
.operator{
  background-color: #f7932e;
  color: #fff;
}
.onDragging .display,
.onDragging .btn,
.onDragging .operator{
    opacity: 0.75;
    cursor: grabbing;
    cursor: -moz-grabbing;
    cursor: -webkit-grabbing;
}
</style>
