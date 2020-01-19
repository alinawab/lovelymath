<template>
<div class="base">
  <div class = "heading">Lovely Math</div>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="recall" class ="btn memorybox">Mrc</div>
    <div @click="clearmem" class ="btn memorybox">M-</div>
    <div @click="addmem" class ="btn memorybox">M+</div>
    <div @click="negate" class ="btn operator">+/-</div>
    <div @click="clear" class ="btn pink">CE/C</div>
    <div @click="append('7')" class ="btn orange">7</div>
    <div @click="append('8')" class ="btn yellow">8</div>
    <div @click="append('9')" class ="btn purple">9</div>
    <div @click="percent" class ="btn operator">%</div>
    <div @click="backspace" class ="btn operator">--></div>
    <div @click="append('4')" class ="btn light-blue">4</div>
    <div @click="append('5')" class ="btn deep-green">5</div>
    <div @click="append('6')" class ="btn red">6</div>
    <div @click="times" class ="btn operator">x</div>
    <div @click="divide" class ="btn operator">/</div>
    <div @click="append('1')" class ="btn pink">1</div>
    <div @click="append('2')" class ="btn orange">2</div>
    <div @click="append('3')" class ="btn yellow">3</div>
    <div @click="plus" class ="btn operator">+</div>
    <div @click="minus" class ="btn operator">-</div>
    <div @click="append('0')" class ="btn purple">0</div>
    <div @click="append('00')" class ="btn red">00</div>
    <div @click="dot" class ="btn light-blue">.</div>
    <div @click="randomNumber" class ="btn randomnumber operator">random number</div>
    <div @click="answer" class ="btn operator">=</div>
  </div>
</div>
</template>

<script>
export default {
  data(){
    return {
      previous: null,
      memory: '',
      current: '',
      operator: null,
      dotClicked: false,
      operatorClicked: false,
    }
  },
  methods: {
    clear (){
      this.current = '';
      this.dotClicked = false;
    },
    randomNumber(){
      this.current = Math.floor(Math.random()*1000);
    },
    negate(){
      this.current = -1 * parseInt(this.current,10);
    },
    backspace(){
      this.current = this.current.slice(0,this.current.length-1);
     
    },
    percent(){
      if (this.current === ''){
        this.clear();
      } else {
        this.current = `${parseFloat(this.current)/100}`;
      }
      
    },
    recall(){
      this.current = this.memory;
    },
    addmem(){
      this.memory = this.current;
      this.clear();
    },
    clearmem(){
      this.memory = '';
      this.clear();
    },
    append(number){
      if (this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot(){
      if (this.dotClicked){
        this.clear();
      }else
      {
        this.append('.');
        this.dotClicked = true;
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide(){
      this.operator = (a,b) => b / a;
      this.setPrevious();
    },
    minus(){
      this.operator = (a,b) => a - b;
      this.setPrevious();

    },
    plus(){
      this.operator = (a,b) => a + b;
      this.setPrevious();

    },
    times(){
      this.operator = (a,b) => a * b;
      this.setPrevious();
    },
    answer(){
      
      if (this.previous === null){
        this.clear();
      }else {
        this.current =`${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
      }
      
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.heading{
  color: white;
  font-size: 40px;
}

.base{
  margin: 0 auto;
  width: 446px;
  height: 463px;
  background-color: #06A2FA;
}

.calculator {
  padding-top: 70px;
  padding: 20px;
  width: 400px;
  font-size:30px;
  display:grid;
  grid-template-columns: repeat(5, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.memorybox{
  background-color: #928F8F;
  color: #FAFF05;
}

.display{
  font-size:50px;
  text-align: right;
  grid-column: 1/6;
  background-color: #F606FB;
  padding-right: 15px;

  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 400px;
  
}

.randomnumber{

  font-size: 20px;
}

.memorybox{
  background-color: #928F8F;
  text-color: #FAFF05;
}

.btn{
  padding: 5px;
  border: 5px solid #06A2FA;

}

.operator {
  background-color: #05FF00;
    padding: 5px;
}

.orange {
  background-color: #FF9900;
}

.yellow {
  background-color: #EAFE00;
}

.red {
  background-color: #FF0000;
}

.pink {
  background-color: #F606FB;
}
.purple {
  background-color: #8000FF;
}
.light-blue {
  background-color: #57C3FF;
}

.deep-green {
  background-color: #00FF38;
}



</style>
