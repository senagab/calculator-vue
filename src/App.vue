<script setup>
import { reactive } from 'vue';

const estado = reactive({
  valorCorrente: '',
  numeroAnterior: null,
  operador: null,
  operadorClicado: false,
});

const backspace = () => {
  estado.valorCorrente = estado.valorCorrente.slice(0, -1);
};

const raizQuadrada = () => {
  estado.valorCorrente = `${Math.sqrt(parseFloat(estado.valorCorrente))}`;
};

const limpar = () => {
  estado.valorCorrente = '';
};

const sinal = () => {
  estado.valorCorrente = estado.valorCorrente.charAt(0) === '-'
    ? estado.valorCorrente.slice(1)
    : `-${estado.valorCorrente}`;
};

const porcentagem = () => {
  estado.valorCorrente = `${parseFloat(estado.valorCorrente) / 100}`;
};

const juntarNumeros = (numero) => {
  if (estado.operadorClicado) {
    estado.valorCorrente = '';
    estado.operadorClicado = false;
  }
  estado.valorCorrente = `${estado.valorCorrente}${numero}`;
};

const ponto = () => {
  if (estado.valorCorrente.indexOf('.') === -1) {
    juntarNumeros('.');
  }
};

const setarValor = () => {
  estado.numeroAnterior = estado.valorCorrente;
  estado.operadorClicado = true;
};

const dividir = () => {
  estado.operador = (num1, num2) => num1 / num2;
  setarValor();
};

const multiplicar = () => {
  estado.operador = (num1, num2) => num1 * num2;
  setarValor();
};

const diminuir = () => {
  estado.operador = (num1, num2) => num1 - num2;
  setarValor();
};

const somar = () => {
  estado.operador = (num1, num2) => num1 + num2;
  setarValor();
};

const resultado = () => {
  estado.valorCorrente = `${estado.operador(
    parseFloat(estado.numeroAnterior),
    parseFloat(estado.valorCorrente)
  )}`;
  estado.numeroAnterior = null;
};

</script>

<template>
  <header>
    <h2>calc-vue</h2>
  </header>
  <!-- CONTAINER -->
  <div class="container">
    <!-- DISPLAY -->
    <div class="display">
      <div class="display__last-operation">
        <span class="display__last-operation__text">
          {{ estado.numeroAnterior }} {{ operadorSimbolo }} =
        </span>
      </div>
      <input maxlength="21" type="text" class="display__text" :value="estado.valorCorrente" readonly>
    </div>

    <!-- TECLADO -->
    <div class="keyboard">
      <div class="keyboard__left">
        <div @click="juntarNumeros(7)" class="keys">7</div>
        <div @click="juntarNumeros(8)" class="keys">8</div>
        <div @click="juntarNumeros(9)" class="keys">9</div>
        <div @click="juntarNumeros(4)" class="keys">4</div>
        <div @click="juntarNumeros(5)" class="keys">5</div>
        <div @click="juntarNumeros(6)" class="keys">6</div>
        <div @click="juntarNumeros(1)" class="keys">1</div>
        <div @click="juntarNumeros(2)" class="keys">2</div>
        <div @click="juntarNumeros(3)" class="keys">3</div>
        <div @click="juntarNumeros(0)" class="keys">0</div>
        <div @click="ponto" class="keys" style="color: gray;">,</div>
        <div @click="raizQuadrada" class="keys" style="color: gray;">√</div>
      </div>
      <div class="keyboard__center">
        <div @click="dividir" class="keys">/</div>
        <div @click="multiplicar" class="keys">x</div>
        <div @click="diminuir" class="keys">-</div>
        <div @click="somar" class="keys">+</div>
      </div>
      <div class="keyboard__right">
        <div @click="backspace" class="keys btn btn-backspace" style="border: none;"></div>
        <div @click="limpar" class="keys">C</div>
        <div @click="resultado" class="keys btn btn-equals" style="height: 21vh;">=</div>
      </div>
    </div>
  </div>
  <!-- FIM DO CONTAINER -->
</template>


<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap');


* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Inter', sans-serif;
}

header {
  color: #bdbdbd;
}

.container {
  display: flex;
  flex-direction: column;
  width: 40%;
  min-width: 35em;
  margin: 0 auto;
  height: 100%;
  background-color: black;
  border-radius: 5px;
}

.display {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 20vh;
  width: auto;
  background-color: #232323;
  margin: 30px;
  border-left: solid 6px #E83D2A;
  border-radius: 5px;
  position: relative;

  .display__last-operation {
    position: absolute;
    top: 20px;
    right: 15px;
    color: rgb(150, 150, 150);
  }

  .display__text {
    width: 500px;
    height: 60px;
    background-color: transparent;
    /* border: solid 1px white; */
    border: none;
    position: absolute;
    bottom: 25px;
    right: 13px;
    font-size: 5em;
    color: white;
    text-align: right;
    font-weight: 500;
    caret-color: transparent;
  }

  .display__text:focus {
    outline: none;
  }
}

.keyboard {
  margin: -15px 30px 30px;
  display: flex;
  justify-content: space-around;

  .keyboard__left {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 1rem;

    .keys {
      width: 10vh;
      height: 10vh;
      /* border: 1px solid #232323; */
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: black;
      font-size: 30px;
      color: white;
    }
    
    .keys:hover {
      background-color: #232323;
      cursor: pointer;
    }
  }

  .keyboard__center {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;

    .keys {
      width: 10vh;
      height: 10vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: black;
      font-size: 30px;
      color: rgb(138, 138, 138);
      /* border: 1px solid #232323; */
    }
    
    .keys:hover {
      background-color: #232323;
      cursor: pointer;
    }
  }

  .keyboard__right {
    display: grid;
    grid-template-columns: 50px;
    grid-template-rows: 1fr 1fr 2fr;
    gap: 1rem;
    margin: 0 15px;

    .keys {
      width: 10vh;
      height: 10vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: black;
      padding: 30px;
      font-size: 30px;
      color: rgb(138, 138, 138);
      /* border: 1px solid #232323; */
    }

    .btn-backspace {
      background-image: url('./assets/images/backspace.svg');
      background-position: center;
      background-repeat: no-repeat;
      background-size: contain;
      padding: 0 !important;
    }

    .btn-equals {
      background-image: url('./assets/images/equals.png');
      background-position: center;
      background-repeat: no-repeat;
      background-size: cover;
      padding: 0 !important;
    }

    .keys:hover {
      background-color: #232323;
      cursor: pointer;
    }
  }
}
</style>
