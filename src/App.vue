<script setup>
import { reactive, ref, onMounted, onUnmounted } from "vue";

const estado = reactive({
  valorCorrente: "",
  ultimaOperacao: "",
  operacaoFinalizada: false,
  soundIndex: 0,

});

const historyDisplay = ref("");

const sons = [
  "./src/assets/sounds/1st - E.mp3",
  "./src/assets/sounds/2nd - A.mp3",
  "./src/assets/sounds/3rd - E.mp3",
  "./src/assets/sounds/4th - B.mp3",
  "./src/assets/sounds/5th - E.mp3",
  "./src/assets/sounds/6th - G.mp3",
  "./src/assets/sounds/7th - A.mp3",
  "./src/assets/sounds/8th - E.mp3",
  "./src/assets/sounds/9th - C2.mp3",
  "./src/assets/sounds/10th - E.mp3",
  "./src/assets/sounds/11th - D2.mp3",
  "./src/assets/sounds/12th - E.mp3",
  "./src/assets/sounds/13th - B.mp3",
  "./src/assets/sounds/14th - C2.mp3",
];

// Função para reproduzir o próximo som
function tocarSom() {
  const somAtual = sons[estado.soundIndex];
  const audio = new Audio(somAtual);
  audio.play();

  // Avança para o próximo som ou reinicia o loop
  estado.soundIndex = (estado.soundIndex + 1) % sons.length;
}

function juntarNumeros(num) {
  if (estado.operacaoFinalizada) {
    estado.valorCorrente = "";
    estado.operacaoFinalizada = false;
  }
  estado.valorCorrente += num;
}

function ponto() {
  const partes = estado.valorCorrente.split(/[\+\-\x\/]/);
  const ultimoNumero = partes[partes.length - 1];

  if (!ultimoNumero.includes(",")) {
    estado.valorCorrente += ",";
  }
}

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

function adicionarOperador(operador) {
  if (estado.operacaoFinalizada) {
    estado.operacaoFinalizada = false;
  }
  const ultimoCaractere = estado.valorCorrente.slice(-1);

  if (["+", "-", "x", "/"].includes(ultimoCaractere)) {
    estado.valorCorrente = estado.valorCorrente.slice(0, -1) + operador;
  } else {
    estado.valorCorrente += operador;
  }
}

function resultado() {
  try {
    const expressao = estado.valorCorrente.replace(/,/g, ".").replace(/x/g, "*");
    const resultado = eval(expressao);

    historyDisplay.value = `${estado.valorCorrente}=`;

    estado.valorCorrente = resultado.toString().replace(/\./g, ",");

    estado.operacaoFinalizada = true;
  } catch (error) {
    estado.valorCorrente = "Erro";
  }
}

function backspace() {
  if (estado.operacaoFinalizada) return;
  estado.valorCorrente = estado.valorCorrente.slice(0, -1);
}

function limpar() {
  estado.valorCorrente = "";
  historyDisplay.value = "";
  estado.operacaoFinalizada = false;

  estado.soundIndex = 0;

  // tocarSom();
}

const handleKeyPress = (event) => {
  const { key } = event;

  const keyMap = {
    '0': '0', '1': '1', '2': '2', '3': '3', '4': '4',
    '5': '5', '6': '6', '7': '7', '8': '8', '9': '9',
    '+': 'somar', '-': 'diminuir', '*': 'multiplicar', '/': 'dividir',
    'Enter': 'resultado', '=': 'resultado', 'Backspace': 'backspace', ',': 'ponto',
    'Escape': 'limpar'
  };

  const buttonId = keyMap[key];
  const buttonElement = document.querySelector(`[data-key="${buttonId}"]`);

  if (buttonElement) {
    buttonElement.classList.add("active");
    setTimeout(() => buttonElement.classList.remove("active"), 100);
  }

  if (!isNaN(key)) {
    juntarNumeros(key);
  } else if (key === ",") {
    ponto();
  } else if (key === "Backspace") {
    backspace();
  } else if (key === "Enter" || key === "=") {
    resultado();
  } else if (key === "+") {
    somar();
  } else if (key === "-") {
    diminuir();
  } else if (key === "*") {
    multiplicar();
  } else if (key === "/") {
    dividir();
  } else if (key === "Escape") {
    limpar();
  }

  tocarSom(); 
};

onMounted(() => {
  window.addEventListener("keydown", handleKeyPress);
});

onUnmounted(() => {
  window.removeEventListener("keydown", handleKeyPress);
});
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
      <input maxlength="21" type="text" class="display__text" :value="estado.valorCorrente" readonly>
    </div>

    <!-- TECLADO -->
    <div class="keyboard">
      <div class="keyboard__left">
        <div @click="juntarNumeros(7)" class="keys" data-key="7">7</div>
        <div @click="juntarNumeros(8)" class="keys" data-key="8">8</div>
        <div @click="juntarNumeros(9)" class="keys" data-key="9">9</div>
        <div @click="juntarNumeros(4)" class="keys" data-key="4">4</div>
        <div @click="juntarNumeros(5)" class="keys" data-key="5">5</div>
        <div @click="juntarNumeros(6)" class="keys" data-key="6">6</div>
        <div @click="juntarNumeros(1)" class="keys" data-key="1">1</div>
        <div @click="juntarNumeros(2)" class="keys" data-key="2">2</div>
        <div @click="juntarNumeros(3)" class="keys" data-key="3">3</div>
        <div @click="juntarNumeros(0)" class="keys" data-key="0">0</div>
        <div @click="ponto" class="keys" style="color: gray;">,</div>
        <div @click="raizQuadrada" class="keys" style="color: gray;">√</div>
      </div>
      <div class="keyboard__center">
        <div @click="dividir" class="keys keys--div" data-key="dividir">/</div>
        <div @click="multiplicar" class="keys keys--mult" data-key="multiplicar">x</div>
        <div @click="diminuir" class="keys keys--sub" data-key="diminuir">-</div>
        <div @click="somar" class="keys keys--sum" data-key="somar">+</div>
      </div>
      <div class="keyboard__right">
        <div @click="backspace" class="keys btn btn-backspace" data-key="backspace" style="border: none;"></div>
        <div @click="limpar" class="keys" data-key="limpar" >C</div>
        <div @click="resultado" class="keys btn btn-equals" data-key="resultado" style="height: 21vh;"></div>
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
  filter: drop-shadow(3px 3px 0.75rem rgba(255, 255, 255, 0.1));
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
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: black;
      font-size: 30px;
      color: rgb(128, 128, 128);
    }
    
    .keys:hover {
      background-color: #1a1a1a;
      color: rgb(206, 206, 206);
      cursor: pointer;
    }

    .keys:active {
      background-color: #2b2b2b;
      color: rgb(255, 255, 255);
      font-weight: bold;
      font-size: 25px;
    }

    .keys.active {
      background-color: #2b2b2b;
      color: rgb(255, 255, 255);
      font-weight: bold;
      font-size: 25px;
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
    }
    
    .keys:hover {
      background-color: #1a1a1a;
      color: rgb(206, 206, 206);
      cursor: pointer;
    }

    .keys:active {
      background-color: #2b2b2b;
      color: rgb(255, 255, 255);
      font-weight: bold;
      font-size: 20px;
    }

    .keys.active {
      background-color: #2b2b2b;
      color: rgb(255, 255, 255);
      font-weight: bold;
      font-size: 25px;
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

    .keys:active {
      background-color: #2b2b2b;
      color: rgb(255, 255, 255);
      font-weight: bold;
      font-size: 25px;
    }

    .keys.active {
      background-color: #2b2b2b;
      color: rgb(255, 255, 255);
      font-weight: bold;
      font-size: 25px;
    }
  }
}
</style>
