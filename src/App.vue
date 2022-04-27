<template>
  <div>
    <div class="display">
      <input v-model.number="operand1" />
      <input v-model.number="operand2" />
      <!-- = {{ fibResult }}; -->
      = {{ result }}
    </div>
    <div v-if="error">{{ error }}</div>
    <!-- <div v-for="(item, index) in myCollections" :key="index" > {{ index }} - {{ item }}</div> -->
    <div class="keyboard">
      <button v-for="operand in operands" @click="calculate(operand)" :key="operand" :title="operand" :disabled="IsNumber()">{{ operand }}</button>
    </div>
    <div v-for="(log,id) in logs" :key="id">{{ log }}</div>
    <br>
    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">Отобразить экранную клавиатуру</label>
    <br>
    <div v-if="checked"> 
      <button @click="pressBtn(number)" v-for="number in buttonNumbers" :key="number">{{ number }}</button>
      <button @click="deleteNumber()"><img src="https://img.icons8.com/glyph-neue/10/000000/long-arrow-left.png"/></button>
    </div>
    <div>
      <input type="radio" name="radioBtn" id="radioOne" value="operand1" v-model="picked">
      <label for="radioOne">Операнд 1</label>
      <input type="radio" name="radioBtn" id="radioTwo" value="operand2" v-model="picked">
      <label for="radioTwo">Операнд 2</label>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator_",
  data() {
    return {
      operand1: 0,
      operand2: 0,
      operands: ['+', '-', '/','*','^'],
      result: 0,
      error:'',
      // myCollections: [1, 2, 3, 4, 5],
      logs: {},
      // fibResult: 0,
      buttonNumbers: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
      checked: false,
      picked: '',
    }
  },
  methods: {
    calculate(operation = "+") {
      this.error ='';
      switch (operation) {
        case "+":
          this.add();
          break;
        case "-":
          this.substract();
          break;
        case "/":
          this.divide()
          break;
        case "*":
          this.multiply();
          break;
        case "^":
          this.pow();
          break;
      }
      const key = Date.now ()
      const value = `${this.operand1}${operation}${this.operand2} = ${this.result}`
      this.$set(this.logs, key, value)
    },

    // fib(n) {
    //   return n <=1 ? n:this.fib(n-1) + this.fib(n-2);
    // },

    add() {
      this.result = +this.operand1 + +this.operand2;
      // this.fibResult = this.fibb1 + this.fibb2;
    },

    substract() {
      this.result = this.operand1 - this.operand2;
      // this.fibResult = this.fibb1 - this.fibb2;
    },

    divide() {
      const {operand1, operand2} = this
      if (operand2 === 0) {
        this.error = "На ноль делить нельзя"
        this.result = 0;
        return
      }
        this.result = operand1 / operand2
    },

    multiply() {
      this.result = this.operand1 * this.operand2;
    },

    pow() {
      this.result = Math.pow(this.operand1, this.operand2);
    },

    IsNumber () {
      return this.operand1 % 1 == 0 && this.operand2 % 1 == 0 ? false : true;
    },

    pressBtn(number) {
      if (this[this.picked] == this.operand1) {
        this.operand1 += number;
      } else {
        this.operand2 += number;
      }
    },

    deleteNumber() {
      if (this[this.picked] == this.operand1) {
        this.operand1 = Array.from(this.operand1);
        this.operand1.pop();
        this.operand1 = this.operand1.join('');
      } else {
        this.operand2 = Array.from(this.operand2);
        this.operand2.pop();
        this.operand2 = this.operand2.join('');
      }
    }

  },

  // computed: {
  //   fibb1() { 
  //     return this.fib(this.operand1)
  //   },
  //   fibb2() { 
  //     return this.fib(this.operand2)
  //   }
  // }
};
</script>

<style lang="scss">
.display {
  input {
    font-size: 20px;
    color: black;
    margin-right: 20px;
    padding: 5px;
    border: 1px solid rgb(186, 66, 190);
    border-radius: 5px;
    outline: none;
  }
}

.keyboard {
  display: flex;
  align-items: center;
  margin-top: 25px;
  margin-left: 110px;
  button {
    display: inline-block;
    margin-right: 20px;
    padding: 15px;
    font-size: 25px;
    text-align: center;
    color: white;
    background-color: rgb(186, 66, 190);
    border: 1px solid rgb(186, 66, 190);
    border-radius: 10px;
  }
}
</style>
