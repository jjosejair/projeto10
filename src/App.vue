<template>
  <div id="app">
    <Calculator />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Calculator from './components/Calculator.vue';

export default defineComponent({
  name: 'App',
  components: {
    Calculator
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #a80c48;
  margin-top: 60px;
}
</style>