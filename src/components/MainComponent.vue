<template>
  <template :key="index" v-for="(log, index) in logs">
    <LineComponent></LineComponent>
  </template>
</template>

<script>
import LineComponent from './LineComponent.vue';

export default {
  name: 'MainComponent',
  components: {
    LineComponent
  },
  data() {
    return {
      invisible : [],
      logs : [],
      isScroll : false
    };
  },
  setup() {
    
  },
  created() {
  },
  mounted() {
    setInterval(this.pushLine,1500);
  },
  unmounted() {
  
  },
  methods: {
    async pushLine() {
      let line = LineComponent;
      this.logs.push(line);
    }
  },
  watch:{

  },
  updated() {
    this.$nextTick(function () {
      // if(window.innerHeight < document.body.clientHeight){
      //   window.addEventListener('scroll', (event) => { 
      //     document.body.style.overflow = 'scroll';
      //     event.target;
      //   });
      // }
      if(window.innerHeight < document.body.scrollHeight){
        window.scrollTo(0,document.body.scrollHeight);
      }

    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  color: white;
}
</style>
