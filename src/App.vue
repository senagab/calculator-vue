<script setup>
/* Importação dos componentes principais */
import { reactive, ref, onMounted, onUnmounted } from "vue";
import Header from './components/Header.vue' // Componente para o cabeçalho da calculadora
import Display from './components/Display.vue' // Componente para exibição dos valores e histórico
import Keyboard from './components/Keyboard.vue' // Componente do teclado da calculadora

/* Função para configurar a cor de fundo da página */
function bgColor() {
  addEventListener("DOMContentLoaded", (event) => {
    document.body.style.backgroundColor = "#1a1a1a";
  });
}
bgColor();



/* Estado reativo para gerenciar os valores da calculadora */
const estado = reactive({
  valorCorrente: "", // Valor atual digitado ou em cálculo
  ultimaOperacao: "", // Última operação realizada
  operacaoFinalizada: false // Indica se uma operação foi finalizada
});

/* Estado reativo para o display de histórico */
const historyDisplay = ref(""); // Mostra a última operação completa

/* Função para adicionar números ao valor corrente */
function juntarNumeros(num) {
  if (estado.operacaoFinalizada) {
    estado.valorCorrente = ""; // Reseta o valor se uma operação foi finalizada
    estado.operacaoFinalizada = false;
  }
  estado.valorCorrente += num; // Concatena número
}

/* Função para adicionar um ponto decimal ao valor corrente */
function ponto() {
  const partes = estado.valorCorrente.split(/[\+\-\x\/]/); // Separa os números por operadores
  const ultimoNumero = partes[partes.length - 1];

  if (!ultimoNumero.includes(",")) { // Adiciona ponto apenas se não houver outro no número atual
    estado.valorCorrente += ",";
  }
}

/* Funções para cada operação matemática */
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

/* Função para adicionar operadores matemáticos */
function adicionarOperador(operador) {
  if (estado.operacaoFinalizada) {
    estado.operacaoFinalizada = false; // Reinicia o estado de finalização 
  }
  const ultimoCaractere = estado.valorCorrente.slice(-1); // Último caractere do valor atual

  if (["+", "-", "x", "/"].includes(ultimoCaractere)) {
    estado.valorCorrente = estado.valorCorrente.slice(0, -1) + operador; // Substitui operador
  } else {
    estado.valorCorrente += operador; // Adicione novo operador
  }
}

/* Função para calcular o resultado da operação */
function resultado() {
  try {
    const expressao = estado.valorCorrente.replace(/,/g, ".").replace(/x/g, "*"); // Formata expressão
    const resultado = eval(expressao); // Calcula resultado

    historyDisplay.value = `${estado.valorCorrente}=`; // Atualiza histórico

    estado.valorCorrente = resultado.toString().replace(/\./g, ","); // Formata resultado

    estado.operacaoFinalizada = true; // Marca operação como finalizada
  } catch (error) {
    estado.valorCorrente = "Erro"; // Exibe erro se houver problema
  }
}

/* Função para apagar o último caractere */
function backspace() {
  if (estado.operacaoFinalizada) return; // Impede edição após finalizar operação
  estado.valorCorrente = estado.valorCorrente.slice(0, -1);
}

/* Função para limpar tudo */
function limpar() {
  estado.valorCorrente = ""; // Reseta valor corrente
  historyDisplay.value = ""; // Reseta o histórico
  estado.operacaoFinalizada = false;
}

/* Função de raiz quadrada */
function raizQuadrada() {
  try {
    const valorAtual = estado.valorCorrente.replace(",", ".");
    if (!valorAtual || isNaN(valorAtual)) {
      estado.valorCorrente = "Erro";
      return;
    }
    const resultado = Math.sqrt(parseFloat(valorAtual));
    historyDisplay.value = `√${valorAtual}=`; // Atualiza o histórico com a operação
    estado.valorCorrente = resultado.toString().replace(".", ","); // Atualiza o display com o resultado
    estado.operacaoFinalizada = true; // Marca a operação como finalizada
  } catch (error) {
    estado.valorCorrente = "Erro"; // Exibe erro se houver problema
  }
}


/* Tratamento de eventos de clique nos botões */
const handleKeyPress = (event) => {
  const { key } = event;

  // Impede repetição contínua da tecla
  if (event.repeat) return;

  handleButtonPress(key, "keyboard");
};

/* Tratamento de eventos de clique nos botões */
const handleButtonClick = (event) => {
  const button = event.target.closest("[data-key]"); // Identifica botão clicado
  if (button) {
    const buttonId = button.getAttribute("data-key");
    handleButtonPress(buttonId, "click");
  }
};

/* Função para tratar entrada de botões ou teclas */
const handleButtonPress = (key, inputType) => {
  const keyMap = {
    '0': '0', '1': '1', '2': '2', '3': '3', '4': '4',
    '5': '5', '6': '6', '7': '7', '8': '8', '9': '9',
    '+': 'somar', '-': 'diminuir', '*': 'multiplicar', '/': 'dividir',
    'Enter': 'resultado', '=': 'resultado', 'Backspace': 'backspace', ',': 'ponto',
    'Escape': 'limpar', 'v': 'raizQuadrada'
  };


  const buttonId = keyMap[key];
  const buttonElement = document.querySelector(`[data-key="${buttonId}"]`);

  if (buttonElement) {
    // Verificar se a ação é para backspace ou resultado, e adicionar as classes corretas
    if (buttonId === 'backspace') {
      buttonElement.classList.add('active-limpar'); // Adiciona estilo ao botão de apagar
    } else if (buttonId === 'resultado') {
      buttonElement.classList.add('active-resultado'); // Adiciona estilo ao botão de resultado
    } else {
      buttonElement.classList.add('active'); // Adiciona estilo genérico
    }

    // Remover a classe após 100ms, aplicando em ambos os tipos de input (teclado e clique)
    setTimeout(() => buttonElement.classList.remove('active', 'active-limpar', 'active-resultado'), 100);
  }

  if (inputType === "click" && !isNaN(key)) return; // Impede duplicidade no clique

  /* Chamadas de funções apropriedas baseadas na entrada */
  if (!isNaN(key)) {
    juntarNumeros(key);
  } else if (key === "," || buttonId === "ponto") {
    ponto();
  } else if (key === "Backspace" || buttonId === "backspace") {
    backspace();
  } else if (key === "Enter" || key === "=" || buttonId === "resultado") {
    resultado();
  } else if (key === "+" || buttonId === "somar") {
    somar();
  } else if (key === "-" || buttonId === "diminuir") {
    diminuir();
  } else if (key === "*" || buttonId === "multiplicar") {
    multiplicar();
  } else if (key === "/" || buttonId === "dividir") {
    dividir();
  } else if (key === "v" || buttonId === "raizQuadrada") {
  raizQuadrada();
  } else if (key === "Escape" || buttonId === "limpar") {
    limpar();
  }
};

/* Adiciona e remove eventos ao montar e desmontar o componente */
onMounted(() => {
  window.addEventListener("keydown", handleKeyPress); // Evento de teclado
  document.addEventListener("click", handleButtonClick); // Evento de clique
});

onUnmounted(() => {
  window.removeEventListener("keydown", handleKeyPress); // Remove evento de teclado
  document.removeEventListener("click", handleButtonClick); // Remove evento de clique
});


</script>

<template>
  <Header />
  <!-- CONTAINER -->
  <div class="container">

    <Display :estado="estado" :historyDisplay="historyDisplay" />
    <Keyboard 
      :juntarNumeros="juntarNumeros"
      :ponto="ponto"
      :somar="somar"
      :diminuir="diminuir"
      :multiplicar="multiplicar"
      :dividir="dividir"
      :backspace="backspace"
      :limpar="limpar"
      :raizQuadrada="raizQuadrada"
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
  color: #525252;
  text-align: center;
}

.container {
  display: flex;
  flex-direction: column;
  width: 60%;
  min-width: 50em;
  height: 100%;
  min-height: 70vh;
  margin: 0 auto 50px;
  background-color: black;
  border-radius: 5px;
  filter: drop-shadow(3px 3px 0.75rem rgba(255, 255, 255, 0.1));
}

@media (max-width: 640px) {
  .container {
    height: 100%;
    max-height: 35em;
    width: 20%;
    min-width: 20em;
  }
}

</style>
