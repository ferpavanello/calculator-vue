<template>
  <div id="app">
    <h1>Calculator</h1>
    <Calculator />
  </div>
</template>

<script>
import Calculator from './main/Calculator'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
  * {
    font-family: "Roboto", sans-serif;
  }

  body {
    margin: 0;
  }

  #app {
    display: flex;
    flex-direction: column;
    height: 100vh;
    justify-content: center;
    align-items: center;
    text-align: center;

    color: #fff;
    background: linear-gradient(90deg, rgba(60,129,213,1) 0%, rgba(75,75,185,1) 50%, rgba(24,18,126,1) 100%);
  }
</style>
