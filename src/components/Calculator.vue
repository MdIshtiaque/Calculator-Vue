<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append(7)" class="btn">7</div>
    <div @click="append(8)" class="btn">8</div>
    <div @click="append(9)" class="btn">9</div>
    <div @click="multiplication" class="btn operator">*</div>
    <div @click="append(4)" class="btn">4</div>
    <div @click="append(5)" class="btn">5</div>
    <div @click="append(6)" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append(1)" class="btn">1</div>
    <div @click="append(2)" class="btn">2</div>
    <div @click="append(3)" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append(0)" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="result" class="btn operator">=</div>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      current: 0,
      previous: null,
      final: 0,
      math: null,
      Operation: false
    }
  },
  methods: {
    clear() {
      this.current = 0;
      this.previous = null;
    },
    sign() {
      this.current > 0 ? this.current = `-${this.current}`
        : this.current = `${this.current}` * -1;
    },
    append(number) {

      this.current == 0 || this.Operation == true ? this.current = `${number}` :
        this.current = `${this.current}${number}`
      this.Operation = false
    },
    dot() {
      if (this.current != 0) {

        this.current.indexOf('.') === -1 ? this.append('.')
          : this.current
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.Operation = true;
    },
    multiplication() {
      this.math = (a, b) => a * b;
      this.setPrevious();

    },
    divide() {
      this.math = (a, b) => a / b;
      this.setPrevious();
    },
    minus() {
      this.math = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.math = (a, b) => parseInt(a) + parseInt(b);
      this.setPrevious();
    },
    percent()
    {
      this.current = this.current/100;
    },
    result() {
      if(this.previous != null)
      this.current = this.math(this.previous, this.current)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.operator {
  background-color: tomato;
}

.btn {
  border: 1px solid cornflowerblue;
  padding: 15px 25px;
  font-size: 24px;
  text-align: center;
  cursor: pointer;
  outline: none;
  background-color: cornflowerblue;
  border: 2px solid;
  border-radius: 5px;
  box-shadow: 0px 9px #999;
  transition: background-color 0.3s ease;
}

.btn:hover {
  background-color: tomato
}

.btn:active {
  background-color: #cabc39;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}

.calculator {
  display: grid;
  margin: 200px auto;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 40px;
  width: 400px;
  height: 600px;
  box-shadow: 10px 10px 10px 10px #888888;
}

.display {
  display: flex;
  justify-content: flex-end;
  grid-column: 1 / 5;
  padding-top: 50px;
  background-color: yellow;
  box-shadow: 0px 8px #999;
}

.zero {
  grid-column: 1/3;
  background-color: #888888;
}

</style>
