<template>
  <div>
    <div class="calculator" >
      <div class="display">{{ display !== '' ? display : '0' }}</div>
      <div v-on:click="clearDisplay" class="button">AC</div>
      <div v-on:click="negativeToggle" class="button">+/-</div>
      <div v-on:click="percentage" class="button">%</div>
      <div v-on:click="divide" class="button orange">/</div>
      <div v-on:click="inputNumber" class="button">7</div>
      <div v-on:click="inputNumber" class="button">8</div>
      <div v-on:click="inputNumber" class="button">9</div>
      <div v-on:click="times" class="button orange">X</div>
      <div v-on:click="inputNumber" class="button">4</div>
      <div v-on:click="inputNumber" class="button">5</div>
      <div v-on:click="inputNumber" class="button">6</div>
      <div v-on:click="minus" class="button orange">-</div>
      <div v-on:click="inputNumber" class="button">1</div>
      <div v-on:click="inputNumber" class="button">2</div>
      <div v-on:click="inputNumber" class="button">3</div>
      <div v-on:click="plus" class="button orange">+</div>
      <div v-on:click="inputNumber" class="button zero">0</div>
      <div v-on:click="dot" class="button">.</div>
      <div v-on:click="result" class="button orange">=</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      display: '',
      operation: null,
      previous: null,
      operatorClicked: false 
    }
  },
  methods: {

    inputNumber(event){
      if(this.operatorClicked)this.display = ''
      if(this.display.length < 12)this.display += event.target.innerHTML
      this.operatorClicked = false
    },

    clearDisplay(){ this.display = '' },

    negativeToggle(){ this.display = (parseFloat(this.display) * -1).toString() },

    percentage(){
      this.display = `${parseFloat(this.display) / 100}`
    },

    dot(){
      if(this.display.indexOf('.') === -1){
        this.display += '.'
      }
    },

    setPrevious(){
      this.previous = this.display
      this.operatorClicked = true
    },

    divide(){
      this.operation = (a, b) => a / b
      this.setPrevious()
    },
    times(){
      this.operation = (a, b) => a * b
      this.setPrevious()
    },
    minus(){
      this.operation = (a, b) => a - b
      this.setPrevious()
    },
    plus(){
      this.operation = (a, b) => a + b
      this.setPrevious()
    },

    result(){
      if(this.previous && this.display.length > 0){
        this.display = this.operation(parseFloat(this.previous), parseFloat(this.display))
        this.previous = null
      }
    }

  }
}
</script>

<style scoped>

h1{
  margin: 0px;
}

.calculator{
  background:rgb(128, 128, 128);
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 2fr 1fr 1fr 1fr 1fr 1fr;
  grid-gap: 2px;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 19px 38px rgba(0,0,0,0.30), 0 15px 12px rgba(0,0,0,0.22);
  width: 40vw;
  min-width: 340px;
  max-width: 400px;
}

.display{
  grid-column-start: 1;
  grid-column-end: 5;
  background: rgba(0, 0, 0, 0.685);
  color: white;
  font-size: 3em;
  display: flex;
  align-items: flex-end;
  justify-content: flex-end;
  padding: 0px 24px;
  font-weight: lighter;
}

.zero{
  grid-column-start: 1;
  grid-column-end: 3;
}

.button{
  background: #D6D6D6;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #2F2F2F;
  font-size: 2em;
  padding: 16px;
  cursor: pointer;
}

.orange{
  background: #F99247;
  color: white;
}

</style>
