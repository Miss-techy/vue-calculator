<template>

<div class="calculator">
  <div class="display"> {{ number || '0' }}</div> <!----displays the number and if the there isn't any number,
  display 0 --->

  <div @click="clear" class="btn clear">C</div>  <!---- clear the display element  ---->
  <div @click="remove" class="btn remove">Del</div>
   <div @click="equal" class="btn operator percent">%</div>
  <div @click="append('7')" class="btn">7</div>
  <div @click="append('8')" class="btn">8</div>
  <div @click="append('9')" class="btn">9</div>
  <div @click="multiplication" class="btn operator">x</div>
  <div @click="append('4')" class="btn">4</div>
  <div @click="append('5')" class="btn">5</div>
  <div @click="append('6')" class="btn">6</div>
  <div @click="subtraction" class="btn operator">-</div>
  <div @click="append('1')" class="btn">1</div>
  <div @click="append('2')" class="btn">2</div>
  <div @click="append('3')" class="btn">3</div>
  <div @click="addition" class="btn operator">+</div>
  <div @click="append('0')" class="btn zero">0</div>
  <div @click="dot" class="btn">.</div>
  <div  @click="division" class="btn operator">/</div>
    <div @click="equal" class="btn operator">=</div>
  
  
  
  

  </div>
  
</template>

<script>

export default {
  data() {
    return{
      prevNum: '',
      number: '',  //number state set to an empty string
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {  //if the btn is clicked, clear the display section
      
      this.number = '';
    },

    append(num) {
      if (this.operatorClicked) {
        this.number = '',
        this.operatorClicked = true;
      }
      this.number = `${this.number}${num}`; // append this.number to num
    },

    remove() {
      this.number = this.number.slice(0, -1); //use the slice method t remove the last num
    },

    setPrevNum() {
      this.prevNum = this.number;
      this.operatorClicked = true
    },

  addition() {
    this.operator = (a, b) => a + b;
    this.setPrevNum();
  },

  subtraction() {
    this.operator = (a, b) => a - b;
    this.setPrevNum();
  },

  multiplication() {
    this.operator = (a, b) => a * b;
    this.setPrevNum();
  },

  division() {
    this.operator = (a, b) => a / b;
    this.setPrevNum();
  },

  dot() {
    if(this.number.indexOf('.') === -1) {
      this.append('.');
    }

  }
,
  equal() {
    this.number = `${this.operator(
      parseFloat(this.prevNum),
      parseFloat(this.number)
      )}`
    this.prevNum = '';
  }
  }
}

</script>


<style scoped>

.calculator{
  margin: 0 auto;
  width: 400px;
  font-size: 20px;
  display:grid;
  grid-template-columns: repeat(4, 1fr);   /*4 columns with equal widths, and repeat them (each have athe same percentage) */
  grid-auto-rows: minmax(50%, auto);  /*put some spacing automatically btwn all the rows, each one shld be 50px in height  */
}

.display{
  grid-column: 1 / 5;  /*start at col 1 and end after col 4, which will take the entire first row */
  background: #333;
  color: white;
}

.clear{
  grid-column: 1 / 2; /*giving it 2 columns */
}

.remove{
grid-column: 2/2;
}

.percent{
  grid-column: 3/5;
}

.btn{
  background: #f2f2f2;
  border:1px solid #999;
  cursor: pointer;
}

.operator{
background: rgb(49, 120, 148);
color: white;
}


</style>