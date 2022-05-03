<template>
  <div id="contatiner">
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

    };
  },
  setup() {
    
  },
  created() {

  },
  mounted() {
    
  },
  unmounted() {
  
  },
  methods: {

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
