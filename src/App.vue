<template>
  <div id="app">
    <Calculator/>
  </div>
</template>

<script>
import Calculator from './components/calculator'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
#app {
  display: flex;
  justify-content: center;
  margin-top: 50px;
  color: white;
}
</style>
