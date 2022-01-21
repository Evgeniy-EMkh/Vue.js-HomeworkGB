<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="text" v-model.number="operand1" />
    <input type="text" v-model.number="operand2" />
    = {{ result }}
    <hr />
    <button @click="result = operand1 + operand2">+</button>
    <button @click="result = operand1 - operand2">-</button>
    <button @click="division">/</button>
    <button @click="multiple(operand1, operand2)">*</button>
    <button @click="pow">pow</button>
    <button @click="floor">floor</button>
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
        operand1: 0,
        operand2: 0,
        result: 0,
      }
    },
    methods: {
      multiple(op1, op2) {
        this.result = op1 * op2
      },
      division() {
        this.result = this.operand1 / this.operand2
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