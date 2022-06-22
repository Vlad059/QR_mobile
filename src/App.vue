<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <select id="select_component" v-model="current_component" @input="sendEvent">
    <option v-for="el in comps" :key="el.index" :value="el">{{ el }}</option>
  </select>
  <component :is="watch_current_component"></component>
</template>

<script>
import QrGenerator from './components/qr_generator.vue'
import QrScanner from './components/qr_scanner.vue'

export default {
  data (){
    return{
      camera_permission: false,
      watch_current_component: 'QrGenerator',
      current_component: 'QrGenerator',
      comps: ['QrScanner', 'QrGenerator']
    }   
  },
  name: 'App',
  watch:{
    current_component(newCurrent, oldCurrent){
      if(newCurrent == 'QrScanner' && !this.camera_permission){      
        this.current_component = oldCurrent;
      }
      else{
        this.watch_current_component = newCurrent;
      }
    }
  },
  methods:{
   sendEvent(e){
    if( e.target.value == 'QrScanner' && !this.camera_permission)
    {
      let select = document.getElementById('select_component');
      select.addEventListener('get_camera', ()=>{
        this.camera_permission = true;
        this.current_component = 'QrScanner';
        this.watch_current_component = 'QrScanner';
        })

      let chosen_qrscanner_e = new CustomEvent('chosen_qrscanner', { bubbles: true});     
      document.dispatchEvent(chosen_qrscanner_e);          
    }
   } 
  },
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
