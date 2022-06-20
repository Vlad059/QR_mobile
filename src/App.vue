<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <select v-model="current_component">
    <option v-for="el in comps" :key="el.index" :value="el">{{ el }}</option>
  </select>
  <component :is="current_component"></component>
</template>

<script>
import QrGenerator from './components/qr_generator.vue'
import QrScanner from './components/qr_scanner.vue'

export default {
  data (){
    return{
      current_component: 'QrScanner',
      comps: ['QrScanner', 'QrGenerator']
    }   
  },
  name: 'App',
  components: {
    QrGenerator,
    QrScanner
  }
}
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
