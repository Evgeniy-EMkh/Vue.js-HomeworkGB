<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="text" v-model.number="operand1" />
    <input type="text" v-model.number="operand2" />
    = {{ result }}

    <hr />
    <div v-if="error">
      {{error}}
    </div>
    <button v-for="(operand, inx) in operands" @click="calculate(operand)" :key="inx">{{operand}}</button>
    <br />
    <br />
    <input type="checkbox" id="checkbox" v-model="checked" @click="checkBox(checked)">
    <label for="checkbox">Отобразить экраннную клавиатуру</label>
    <br />
    <div v-if="checked">
      <button v-for="(number, inx) in numbers" @click="addNumbers(number)" :key="inx">{{number}}</button>
      <br />
      <br />
      <input type="radio" id="one" value="operand1" v-model="picked">
      <label for="one">Операнд1</label>
      <input type="radio" id="two" value="operand2" v-model="picked">
      <label for="two">Операнд2</label>
      <br />
    </div>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    props: {
      msg: String
    },
    data() {
      return {
        message: "Hello Vue",
        picked: 'operand1',
        checked: true,
        operand1: '',
        operand2: '',
        result: 0,
        error: '',
        operands: ["+", "-", "*", "/", "pow", "floor"],
        numbers: ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "delete"],
      }
    },
    methods: {
      addNumbers(numberss) {
        if (numberss == "delete") {
          this.deleteLastElement(this.picked)
          return
        } else {
          if (this.picked == "operand1") {
            this.operand1 = this.operand1 + numberss;
          } else {
            this.operand2 = this.operand2 + numberss;
          }
        }
      },

      deleteLastElement(picked) {
        if (picked == "operand1") {
          this.operand1 = this.operand1.slice(0, -1)
        } else {
          this.operand2 = this.operand2.slice(0, -1)
        }
      },

      calculate(operation = "+") {
        switch (operation) {
          case '+':
            this.add()
            break;
          case '-':
            this.substract()
            break;
          case '*':
            this.multiple()
            break;
          case '/':
            this.division()
            break;
          case 'pow':
            this.pow()
            break;
          case 'floor':
            this.floor()
            break;
        }
      },

      add() {
        this.result = Number(this.operand1) + Number(this.operand2)
      },
      substract() {
        this.result = this.operand1 - this.operand2
      },
      multiple() {
        this.result = this.operand1 * this.operand2
      },
      division() {
        const { operand1, operand2 } = this
        if (operand2 == 0) {
          this.error = "На ноль делить нельзя!"
          return
        }
        this.result = operand1 / operand2
      },
      pow() {
        this.result = Math.pow(this.operand1, this.operand2)
      },
      floor() {
        this.result = Math.floor(this.operand1 / this.operand2)
      },
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h3 {
    margin: 40px 0 0;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
</style>