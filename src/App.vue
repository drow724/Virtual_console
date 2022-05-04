<template>
  <div id="contatiner" :key="index" v-for="(component, index) in main">
    <MainComponent></MainComponent>
  </div>
</template>

<script>
import MainComponent from './components/MainComponent.vue'

export default {
  name: 'App',
  components: {
    MainComponent
  },
  data() {
    return {
      main : []
    };
  },
  setup() {
    
  },
  created() {

  },
  mounted() {
    setTimeout(this.pushLine,1500);
  },
  unmounted() {
  
  },
  methods: {
    async pushLine() {
      let line = MainComponent;
      this.main.push(line);
    }
  },
  watch:{

  }
}
</script>

<style>
body::-webkit-scrollbar{
  display: none;
}
body {
  overflow: hidden;
  background-color : black;
  font-family : 'consolab';
  font-size: 13px;
}
@font-face {
  font-family:'consola';
  src: url('assets/fonts/consola.ttf') format('truetype');
  font-weight: 400;
}
@font-face {
  font-family:'consolab';
  src: url('assets/fonts/consolab.ttf') format('truetype');
  font-weight: 300;
}
@font-face {
  font-family:'consolai';
  src: url('assets/fonts/consolai.ttf') format('truetype');
  font-weight: 700;
}
@font-face {
  font-family:'consolaz';
  src: url('assets/fonts/consolaz.ttf') format('truetype');
  font-weight: 700;
}
</style>
