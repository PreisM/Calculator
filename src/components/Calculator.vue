<template>
  <div class="calculator">
    <div class="display">{{current || '-'}}</div>
    <div @click="clear" class="btn">AC</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">,</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: ``,
      operator: ``,
      operatorClicked: false
    };
  },
  methods: {
    // czyszczenie wyniku
    clear() {
      this.current = "";
    },
    // znak minus
    sign() {
      this.current *= -1;
    },
    // procenty
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    // cyfry
    append(number) {
      if (this.operatorClicked) {
        //czyszczenie po wybraniu operatora i kolejnej cyfry
        this.current = "";
        this.operatorClicked = false;
      }
      this.current += number;
    },
    // przecinek/kropka
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    // kliknięcie operatora
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    //operator dzielenia
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    //operator mnożenia
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    //operator odejmowania
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    //operator dodawania
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    // wynik
    equal() {
      this.current = this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      );
      this.previous = "";
    }
  }
};
</script>

<style scoped>
.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: 40vh;
  margin: 20vh auto;
  text-align: center;
  border-radius: 20px;
  box-shadow: 5px 5px 40px -2px hsl(210, 12%, 47%);
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.display {
  font-size: 40px;
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  background-color: #f2f2f2;
  border: 1px solid #999;
  padding: 2.5vh 0;
  cursor: pointer;
}

.btn:active {
  transform: scale(0.97);
}

.operator {
  background-color: rgb(212, 164, 6);
  color: white;
}
</style>
