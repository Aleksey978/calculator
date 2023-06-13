<script>
export default {
  data () {
    return {
      result: '',
      numbers: [1,2,3,4,5,6,7,8,9,0,'.'],
      operations: ['+','-','*','/'],
      operations2: ['(',')'],
      history: []
    }
  },
  methods: {
    input (char) {
      this.result = this.result.toString()
      this.result += char
    },
    reset () {
      this.result = ''
    },
    calc() {
      if (this.result) {
        const expression = this.result;
        const result = eval(expression);
        this.history.push({ expression, result });
        this.result = result;
      }
      
    },
    degree () {
      const base = this.result;
     this.result *= this.result;
      this.history.push({ expression: `${base}<sup>2</sup>`, result: this.result });
    },
    deleteLastChar() {
    this.result = this.result.slice(0, -1);
    },
    clearHistory() {
      this.history = []
    }
  }
}
</script>

<template>
  <div>
    <div class="grid">
    <input @keyup.enter="calc()" class="input" type="text" onkeyup="this.value = this.value.replace (/[^0-9+]/, '')" v-model="result" placeholder="0">
    
      <div class="operations">
        <button @click="input(op)" :key="op" class="cell" v-for="op in operations">{{ op }}</button>
      </div>
      <div class="numbers">
        <button @click="input(num)" :key="num" class="cell num" v-for="num in numbers">{{ num }}</button>
      </div>
      <div class="operations">
        <button @click="deleteLastChar()" class="cell" >C</button>
        <button @click="reset()" class="cell" >R</button>
        <button @click="input(op)" :key="op" class="cell" v-for="op in operations2">{{ op }}</button>
      </div>
      <button @click="degree()" class="cell fraction">X<sup>2</sup></button>
     <button @click="calc()" class="cell" >=</button>
  </div>
      <div class="history__list">
        <div v-if="this.history.length === 0" class="history__item">
          История пуста
        </div>
        <div v-else v-for="item in history" :key="item" class="history__item">
          <span v-html="item.expression"></span> = {{ item.result }}
        </div>
        <button @click="clearHistory()" class="history__btn" v-show="this.history.length !== 0">Очистить историю</button>
      </div>
  </div>
  
</template>

<style scoped>
.grid {
  width: 100%;
  background: #D2DAFF;
  border: 2px solid #B1B2FF;
  padding: 62px 32px;
  box-shadow: 10px 10px #B1B2FF;
  border-radius: 120px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
.cell {
  color: #FF9494;
  font-size: 25px;
  font-weight: bold;
  flex: 20%;
  background: #EEF1FF;
  border: 2px solid #FF9494;
  height: 108px;
  transition: 0.5s all;
  border-radius: 100px;
  margin-right: 15px;
  margin-top: 15px;
  user-select: none;
  position: relative;
  overflow: visible;
  z-index: 2;
  box-shadow: 6px 6px #FF9494;
}

.cell:active {
  box-shadow: 0 0;
  transform: translate(6px, 6px);
}

.num {
  box-shadow: 6px 6px #B1B2FF;
  background: #EEF1FF;
  border: 2px solid #B1B2FF;
  color: #B1B2FF;
}
.cell:hover {
  opacity: 0.7;
}
.input {
  font-size: 30px;
  width: 100%;
  font-weight: 700;
  height: 70px;
  text-align: right;
  padding: 16px 24px 16px 16px;
  border: none;
  border-radius: 50px;
  padding-right: 20px;
  outline: none;
}

.history__list {
  position: absolute;
  top: 20px;
  right: 40px;
}

.history__btn {
  background: none;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: -20px;
  margin-top: -22px;
    position: absolute;
}

.history__item {
  text-align: center;
  align-items: center;
  color:  #575757;
  font-size: 25px;
  margin-bottom: 34px;
  width: 250px;
  padding: 51px 0;
  background: #FFFACF;
  border: 2px solid #FFF490;
  box-shadow: 6px 6px #FFF490;
  border-radius: 80px;
}
.operations {
  flex: 20%;
  display: flex;
  flex-direction: column;
}
.numbers {
  flex: 60%;
  display: flex;
  flex-wrap: wrap;
  /* flex-direction: column; */
}
.numbers .cell {
  flex: 25%;
  /* display: flex;
  flex-wrap: wrap; */
  /* flex-direction: column; */
}
</style>
