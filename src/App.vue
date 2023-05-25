<script>
export default {
  data () {
    return {
      result: '',
      numbers: [1,2,3,4,5,6,7,8,9,0],
      operations: ['+','-','*','/','(',')']
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
    calc () {
      this.result = eval(this.result)
    },
    degree () {
      this.result *= this.result
    }
  }
}
</script>

<template>
  <div class="grid">
    <input @keyup.enter="calc()" class="input" type="text" v-model="result" placeholder="0">
    <button @click="input(num)" class="cell num" v-for="num in numbers">{{ num }}</button>
    <button @click="input(op)" class="cell" v-for="op in operations">{{ op }}</button>
    <button @click="degree()" class="cell fraction">X</button>
    <button @click="reset()" class="cell" >R</button>
    <button @click="calc()" class="cell" >=</button>
  </div>

</template>

<style scoped>
.grid {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
.cell {
  color: white;
  font-size: 25px;
  flex: 30%;
  background-color: rgb(75, 59, 59);
  height: 100px;
  border: none;
  transition: 0.5s all;
  border-radius: 100px;
  margin-right: 5px;
  margin-top: 5px;
  user-select: none;
}
.num {
  background-color: rgb(58, 58, 58);
}
.cell:hover {
  opacity: 0.5;
}
.input {
  font-size: 30px;
  width: 100%;
  height: 70px;
  text-align: right;
  padding: 0;
  border: none;
  border-radius: 50px;
  padding-right: 20px;
  outline: none;
}
.fraction {
  position: relative;
}
.fraction::after {
  content: '2';
  font-size: 12px;
  position: absolute;
  top: 26px;
  right: 67px;
}
</style>
