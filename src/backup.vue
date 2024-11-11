<script setup>
import { reactive, ref } from "vue";

const estado = reactive({
  valorCorrente: "",      // Armazena o valor atual que está sendo digitado/exibido
  ultimaOperacao: "",     // Armazena a última operação para exibição no display de histórico
  operacaoFinalizada: false,  // Indica se uma operação foi finalizada (após o enter)
});

const historyDisplay = ref(""); // Display do histórico

// Função para juntar números no display principal
function juntarNumeros(num) {
  if (estado.operacaoFinalizada) {
    estado.valorCorrente = ""; // Limpa o valorCorrente se uma nova operação começou
    estado.operacaoFinalizada = false;
  }
  estado.valorCorrente += num;
}

// Função para adicionar ponto (decimal)
function ponto() {
  if (!estado.valorCorrente.includes(".")) {
    estado.valorCorrente += ".";
  }
}

// Operações matemáticas
function somar() {
  adicionarOperador("+");
}
function diminuir() {
  adicionarOperador("-");
}
function multiplicar() {
  adicionarOperador("x");
}
function dividir() {
  adicionarOperador("/");
}

// Função para adicionar um operador ao valorCorrente
function adicionarOperador(operador) {
  if (estado.operacaoFinalizada) {
    estado.operacaoFinalizada = false;
  }
  if (!["+", "-", "x", "/"].includes(estado.valorCorrente.slice(-1))) {
    estado.valorCorrente += operador;
  }
}

// Função para calcular o resultado
function resultado() {
  try {
    // Substitui "x" por "*" para a avaliação e calcula
    const expressao = estado.valorCorrente.replace(/x/g, "*");
    const resultado = eval(expressao);

    // Atualiza o display de histórico e exibe o resultado no display principal
    historyDisplay.value = `${estado.valorCorrente}=`;
    estado.valorCorrente = resultado.toString();

    // Marca a operação como finalizada para que a próxima entrada comece uma nova operação
    estado.operacaoFinalizada = true;
  } catch (error) {
    estado.valorCorrente = "Erro";
  }
}

// Função de backspace
function backspace() {
  if (estado.operacaoFinalizada) return;
  estado.valorCorrente = estado.valorCorrente.slice(0, -1);
}

// Função de limpar
function limpar() {
  estado.valorCorrente = "";
  historyDisplay.value = "";
  estado.operacaoFinalizada = false;
}
</script>

<template>
  <header>
    <h2>calc-vue</h2>
  </header>
  <!-- CONTAINER -->
  <div class="container">
    <!-- DISPLAY -->
    <div class="display">
      <!-- Display de Histórico -->
      <div class="display__last-operation">
        <span class="display__last-operation__text">
          {{ historyDisplay }}
        </span>
      </div>
      <!-- Display Principal -->
      <!-- <input maxlength="21" type="text" class="display__text" :value="estado.valorCorrente" readonly> -->
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
