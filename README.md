# calc-vue

<p align="left">
    <img src="https://img.shields.io/badge/vue-v3.5.12-359369?logo=vue.js&labelColor=white" alt="Vue version">
    <img src="https://img.shields.io/badge/vite-v5.4.10-6568FF?logo=vite&labelColor=white" alt="Vite version">
</p>

A calculator web application built with Vue.js, designed for real-time calculations with a sleek, modern interface. This calculator performs basic arithmetic operations and keeps a history of recent calculations, providing both keyboard and clickable interface support.


![Screenshot Home](https://github.com/senagab/servidores-estaticos/blob/main/calc.png)

## Features

- **Real-time Calculation**: Automatically performs calculations as values and operators are entered, with results shown instantly.
- **History Display**: Displays the full expression (e.g., `4x4=`) when the result is calculated, maintaining a history of recent calculations.
- **Keyboard Support**: Supports keyboard inputs for numbers, operators, and control keys like Enter, Backspace, and Escape.
- **Clear and Backspace Functions**: Easily clear all or remove the last entry.
- **Decimal Support**: Allows decimal point entry for more precise calculations.

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) and [Vue CLI](https://cli.vuejs.org/) should be installed.

### Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/calc-vue.git
    cd calc-vue
    ```
2. Install dependencies:
    ```bash
    npm install
    ```
3. Run the application:
    ```bash
    npm run serve
    ```
4. Visit `http://localhost:8080` to view the app in your browser.

## Usage

### Controls

- **Number Buttons (0-9)**: Click or type numbers to input values.
- **Operators (+, -, x, /)**: Add operators to your current calculation.
- **Equal (`=` or Enter)**: Finalize and display the result, updating the history.
- **Clear (C)**: Clears the display and resets the calculator.
- **Backspace**: Deletes the last character in the current input.
- **Keyboard Shortcuts**:
  - **Enter** or **`=`**: Calculate result
  - **Escape**: Clear all
  - **Backspace**: Remove last character

### Example Usage

1. Enter numbers and operators as you type or click.
2. The calculator performs operations in real-time, showing partial results.
3. Press Enter or `=` to see the final result, which will also be displayed in the history.
4. Begin a new calculation, which will automatically reset the display.

## Project Structure

- **Main Components**:
  - `estado`: Reactive state management for the calculator's current value and operations.
  - `historyDisplay`: Shows the last completed calculation.
  - `handleKeyPress`: Event listener to handle keyboard inputs.
  
- **Functions**:
  - **juntarNumeros(num)**: Concatenates number inputs.
  - **ponto()**: Adds a decimal point.
  - **adicionarOperador(op)**: Adds operators (`+`, `-`, `x`, `/`) as inputs.
  - **resultado()**: Calculates and displays the final result.
  - **backspace()**: Removes the last character.
  - **limpar()**: Resets the calculator state.

## Styling

The application is styled with a modern dark theme:
- **Display**: Shows the current calculation in a large, right-aligned font.
- **Keyboard Layout**: Organized in a grid layout with left, center, and right groups for numbers, operators, and control functions.

## License

MIT License. See `LICENSE` file for details.

## Acknowledgments

- Icons for backspace and equals buttons are custom-designed for this calculator.
- Uses the Inter font from Google Fonts for a clean, professional look.

Feel free to fork and customize the calculator as needed!
