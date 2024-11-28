<script setup>
import { reactive, ref, onMounted, onUnmounted } from "vue";
import Header from './components/Header.vue'
import Display from './components/Display.vue'
import Keyboard from './components/Keyboard.vue'

const estado = reactive({
  valorCorrente: "",
  ultimaOperacao: "",
  operacaoFinalizada: false,
});

const historyDisplay = ref("");

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
};

onMounted(() => {
  window.addEventListener("keydown", handleKeyPress);
});

onUnmounted(() => {
  window.removeEventListener("keydown", handleKeyPress);
});
</script>

<template>
  <Header />
  <!-- CONTAINER -->
  <div class="container">
    <!-- DISPLAY -->
    <Display/>

    <!-- TECLADO -->
    <Keyboard
      :juntarNumeros="juntarNumeros"
      :ponto="ponto"
      :somar="somar"
      :diminuir="diminuir"
      :multiplicar="multiplicar"
      :dividir="dividir"
      :backspace="backspace"
      :limpar="limpar"
      :resultado="resultado"
    />
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


</style>
