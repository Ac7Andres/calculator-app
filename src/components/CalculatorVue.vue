<template>
    <div class="calculator">
      <h1>Calculadora Vue</h1>
      <div class="input-container">
        <input type="text" v-model="num1" @input="validateInput($event, 'num1')" placeholder="Número 1">
        <input type="text" v-model="num2" @input="validateInput($event, 'num2')" placeholder="Número 2">
      </div>
      <div class="button-container">
        <button @click="performOperation('+')">Suma</button>
        <button @click="performOperation('-')">Resta</button>
        <button @click="performOperation('*')">Multiplicación</button>
        <button @click="performOperation('/')">División</button>
      </div>
      <p v-if="errorMessage" class="error">{{ errorMessage }}</p>
      <p v-if="result !== null" class="result">Resultado: {{ result }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        num1: '',
        num2: '',
        result: null,
        errorMessage: ''
      };
    },
    methods: {
      validateInput(event, field) {
        // Asegura que solo se ingresen números válidos
        this[field] = event.target.value.replace(/[^0-9.]/g, '');
      },
      performOperation(operation) {
        const number1 = parseFloat(this.num1);
        const number2 = parseFloat(this.num2);
  
        if (isNaN(number1) || isNaN(number2)) {
          this.errorMessage = 'Por favor, ingrese números válidos.';
          this.result = null;
          return;
        }
  
        this.errorMessage = '';
  
        switch (operation) {
          case '+':
            this.result = number1 + number2;
            break;
          case '-':
            this.result = number1 - number2;
            break;
          case '*':
            this.result = number1 * number2;
            break;
          case '/':
            if (number2 === 0) {
              this.errorMessage = 'No se puede dividir por cero.';
              this.result = null;
            } else {
              this.result = number1 / number2;
            }
            break;
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .calculator {
    background-color: #2ecc71; /* Fondo verde */
    min-height: 100vh; /* Altura mínima del 100% de la ventana */
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  
  /* Estilos para los campos de entrada */
  .input-container {
    margin-bottom: 20px;
  }
  
  .input-container input {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 16px;
  }
  
  /* Estilos para los botones */
  .button-container button {
    padding: 10px 20px;
    margin-right: 10px;
    border: none;
    border-radius: 5px;
    background-color: #3498db;
    color: #fff;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .button-container button:hover {
    background-color: #2980b9;
  }
  
  /* Estilos para los mensajes de error y resultados */
  .error, .result {
    font-size: 18px;
    margin-top: 10px;
  }
  
  .error {
    color: #e74c3c;
  }
  
  .result {
    color: #000000;
  }  </style>
  