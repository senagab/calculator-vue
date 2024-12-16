# Calc-Vue

<p align="left">
    <img src="https://img.shields.io/badge/vue-v3.5.12-359369?logo=vue.js&labelColor=white" alt="Vue version">
    <img src="https://img.shields.io/badge/vite-v5.4.10-6568FF?logo=vite&labelColor=white" alt="Vite version">
</p>

A **Calc-Vue** é uma aplicação web de calculadora construída com Vue.js, projetada para cálculos em tempo real com uma interface moderna e amigável. Ideal para tarefas rápidas e precisão em cálculos, a calculadora oferece suporte a teclados e botões clicáveis, além de manter um histórico de operações recentes.

![Screenshot Home](https://github.com/senagab/servidores-estaticos/blob/main/calc.png)

---

## ✨ Features

- **Cálculo em Tempo Real**: Resultados exibidos instantaneamente conforme números e operadores são inseridos.
- **Histórico de Operações**: Exibe o cálculo completo (e.g., `4x4=`) e mantém as últimas operações realizadas.
- **Suporte ao Teclado**: Aceita entradas diretamente do teclado, incluindo números, operadores e funções de controle.
- **Funções Extras**: 
  - Limpeza (C): Reseta todos os valores.
  - Backspace: Remove o último caractere.
  - Raiz Quadrada: Calcula a raiz quadrada do número atual.
- **Compatibilidade com Decimais**: Aceita ponto decimal para cálculos precisos.
- **Estilo Responsivo**: Interface adaptável para diferentes tamanhos de tela.

---

## 🛠️ Tecnologias Utilizadas

- **Vue.js (v3.5.12)**: Framework JavaScript para construção de interfaces reativas.
- **Vite (v5.4.10)**: Ferramenta de build rápida para projetos modernos em JavaScript.
- **CSS Customizado**: Tema escuro moderno com design responsivo.

---

## 🚀 Como Começar

### Pré-requisitos

- [Node.js](https://nodejs.org/) instalado em sua máquina.
- Familiaridade com [Vue CLI](https://cli.vuejs.org/) (opcional).

### Instalação

1. Clone este repositório:
    ```bash
    git clone https://github.com/senagab/calculator-vue.git
    cd calc-vue
    ```
2. Instale as dependências:
    ```bash
    npm install
    ```
3. Inicie o servidor local:
    ```bash
    npm run dev
    ```
4. Acesse a aplicação no navegador:
    ```
    http://localhost:3000
    ```

---

## 🖥️ Como Usar

### Controles

- **Números (0-9)**: Clique ou digite para adicionar valores.
- **Operadores (+, -, x, /)**: Escolha a operação desejada.
- **Igual (`=` ou Enter)**: Finaliza o cálculo e atualiza o histórico.
- **Limpar (C)**: Reseta todos os valores e limpa o histórico.
- **Backspace**: Apaga o último caractere inserido.
- **Raiz Quadrada (V)**: Retorna raiz quadrada do valor digitado.
- **Teclado**:
  - `Enter`: Calcula o resultado.
  - `Backspace`: Apaga o último valor.
  - `Escape`: Limpa tudo.

---

## 🌟 Demonstração

Caso tenha uma versão publicada, inclua o link:
[Demo Online](#).

---

## 🏗️ Estrutura do Projeto

### Principais Componentes

- **Header**: Título e cabeçalho estilizado.
- **Display**: Mostra os valores e o histórico.
- **Keyboard**: Teclado virtual para inserir valores e operadores.

### Principais Funções

- **juntarNumeros(num)**: Adiciona números ao display.
- **ponto()**: Insere um ponto decimal, se válido.
- **adicionarOperador(op)**: Define operadores e evita duplicidades.
- **resultado()**: Realiza o cálculo final.
- **backspace()**: Remove o último caractere.
- **limpar()**: Reseta o estado atual da calculadora.
- **raizQuadrada()**: Calcula a raiz quadrada do valor atual.

---

## 🧪 Testando a Aplicação

1. Siga os passos de instalação e execução.
2. Realize operações básicas para validar o funcionamento.
3. Verifique o histórico e os cálculos para confirmar os resultados.

---

## 🛠️ Contribuindo

Contribuições são bem-vindas! Siga os passos abaixo:

1. Faça um fork do repositório.
2. Crie uma nova branch com suas alterações:
    ```bash
    git checkout -b feature/sua-funcionalidade
    ```
3. Commit suas mudanças:
    ```bash
    git commit -m 'Adiciona nova funcionalidade'
    ```
4. Envie as alterações:
    ```bash
    git push origin feature/sua-funcionalidade
    ```
5. Abra um Pull Request.

---

## 📜 Licença

Este projeto está licenciado sob a [MIT License](./LICENSE).

---

## 🙌 Agradecimentos

- Ícones personalizados para botões e tema.
- Fonte Inter, disponível via [Google Fonts](https://fonts.google.com/specimen/Inter).

---
