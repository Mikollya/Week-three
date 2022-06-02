<template>
  <div class="main">
      <div class="main__inputs">
        <EventListener :value="firstNumber" type="number" @arithmetic="setFisrtNumber"/>
        <EventListener :value="arithmeticSign" type="input" @arithmetic="setArithmeticSign"/>
        <EventListener :value="secondNumber" type="number" @arithmetic="setSecongNumber"/>
      </div>
      <h1> result:
        {{calculate(Number(firstNumber), Number(secondNumber), arithmeticSign)}}
      </h1>
      <span>
        you can choose:
          + - * / ** or %
      </span>
    </div>
</template>

<script>
import EventListener from './components/EventListener.vue'

export default {
  name: 'App',
  components: {
    EventListener
  },
  data() {
    return {
      firstNumber: '0',
      secondNumber: '0', 
      arithmeticSign: '+'
    }
  },
  methods: {
    setFisrtNumber (event) {
      this.firstNumber = event.target.value;
    },
    
    setSecongNumber (event) {
      this.secondNumber = event.target.value;
    },

    setArithmeticSign (event) {
      this.arithmeticSign = event.target.value;
    },

    calculate (firstNumber, secondNumber, arithmeticSign) {
      switch (arithmeticSign) {
        case '+':
          return firstNumber + secondNumber
        case '-': 
          return firstNumber - secondNumber
        case '*':
          return firstNumber * secondNumber
        case '/':
          return firstNumber / secondNumber
        case '**':
          return firstNumber ** secondNumber
        case '%':
          return firstNumber % secondNumber
        default:
          return 0;
      }
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  justify-content: center;
}
.main {
  display: flex;
  flex-direction: column;
  border-radius: 30px;
  color: #2c3e50;
  margin-top: 40px;
  text-align: center;
  background-color: antiquewhite;
  padding-bottom: 20px;
  width: 450px;
}
.main__inputs {
  display: flex;
  flex-direction: row;
  justify-content: center;
  padding: 15px;
}
span {
  font-size: 18px;
}
</style>
