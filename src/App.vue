<template>
  <div>
    <div class="wrapper">
      <div class="answer">{{current || '0'}}</div>
      <div @click="clear" class="btn">С</div>
      <div @click="sign" class="btn">+/-</div>
      <div @click="precent" class="btn">%</div>
      <div @click='divide' class="btn operator">/</div>
      <div @click='append("7")' class="btn">7</div>
      <div @click='append("8")' class="btn">8</div>
      <div @click='append("9")' class="btn">9</div>
      <div @click='times' class="btn operator">x</div>
      <div @click='append("4")' class="btn">4</div>
      <div @click='append("5")' class="btn">5</div>
      <div @click='append("6")' class="btn">6</div>
      <div @click='minus' class="btn operator">-</div>
      <div @click='append("1")' class="btn">1</div>
      <div @click='append("2")' class="btn">2</div>
      <div @click='append("3")' class="btn">3</div>
      <div @click="add" class="btn operator">+</div>
      <div @click='append("0")' class="btn zero">0</div>
      <div @click='dot' class="btn">.</div>
      <div @click='equel' class="btn operator">=</div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        current: '',
        operator: null,
        previous: null,
        operatorClicked: false,
      }
    },
    methods: {
      clear(){
        this.current = '';
      },
      sign(){
        this.current = this.current.charAt(0) === '-' ?
          this.current.slice(1) : `-${this.current}`
      },
      precent(){
        this.current = `${parseFloat(this.current) / 100}`
      },
      append(number){
        if(this.operatorClicked){
          this.current = '';
          this.operatorClicked = false;
        }
        this.current = `${this.current}${number}`
      },
      dot(){
        if(this.current.indexOf('.') === -1){
          this.append('.')
        }
      },
      setPrevious(){
        this.previous = this.current;
        this.operatorClicked = true;
      },
      divide() {
        this.operator = (a, b) => b / a;
        this.setPrevious();
      },
      times(){
        this.operator = (a, b) => b * a;
        this.setPrevious();
      },
      minus(){
        this.operator = (a, b) => b - a;
        this.setPrevious();
      },
      add(){
        this.operator = (a, b) => b + a;
        this.setPrevious();
      },
      equel(){
        this.current = `${this.operator(
          parseFloat(this.current), 
          parseFloat(this.previous)
        )}`;
        this.previous = null;
      }
    }
  }
</script>

<style>
.wrapper {
  text-align: center;
  font-size: 30px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: 400px;
  margin: 0 auto;
  line-height: 2em;
}
.answer {
  grid-column: 1/5;
  background-color: #333;
  color: #fff;
}

.zero {
  grid-column: 1/3;
}

.btn {
  background-color: #f2f2f2;
  border: 1px solid #999;
  cursor: pointer;
}

.btn:hover {
  background-color: #d3d0d0;
}

.operator {
  background-color: orange;
  color: #fff;
}
</style>