<template>
    <div class="calculator">
      <input v-model="display" readonly class="display" />
      <div class="buttons">
        <button
          v-for="button in buttons"
          :key="button"
          @click="handleClick(button)"
          :class="{'operator': isOperator(button)}"
        >
          {{ button }}
        </button>
      </div>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref } from 'vue';
  import { evaluate } from 'mathjs';
  
  export default defineComponent({
    name: 'Calculator',
    setup() {
      const display = ref('');
      const lastInput = ref('');
  
      const buttons = [
        '7', '8', '9', '/',
        '4', '5', '6', '*',
        '1', '2', '3', '-',
        '0', '.', '=' , '+',
        'C',                    
                   
     
      ];
  
      const handleClick = (button: string) => {
        if (button === 'C') {
          display.value = '';
          lastInput.value = '';
        } else if (button === '=') {
          try {
            display.value = evaluate(display.value).toString();
            lastInput.value = display.value;
          } catch (e) {
            display.value = 'Error';
            lastInput.value = '';
          }
        } else {
          if (display.value === 'Error') display.value = '';
          if (isOperator(button)) {
            if (isOperator(lastInput.value)) {
              display.value = display.value.slice(0, -1);
            }
            if (display.value === '') return;
          }
          display.value += button;
          lastInput.value = button;
        }
      };
  
      const isOperator = (button: string) => {
        return ['/', '*', '-', '+'].includes(button);
      };
  
      return {
        display,
        buttons,
        handleClick,
        isOperator
      };
    }
  });
  </script>
  
  <style scoped>
  .calculator {
    max-width: 200px;
    margin: 50px auto;
    text-align: center;
    border: 1px solid black;
    padding: 10px;
    border-radius: 15px;
    background-color: rgb(60, 60, 60);
  }
  
  .display {
    width: 100%;
    height: 60px;
    margin-bottom: 10px;
    font-size: 2em;
    text-align: right;
    background-color: rgb(252, 245, 245);
    color: rgb(51, 53, 53);
    padding: 5px;
    box-sizing: border-box;
    border-radius: 10px;
  }
  
  .buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
  }
  
  button {
    width: 100%;
    height: 50px;
    font-size: 2.5em;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  button.operator {
    background-color: rgb(8, 8, 8);
    color: rgb(5, 19, 218);
  }
  
  button:hover {
    background-color: rgb(248, 211, 3);
  }
  </style>