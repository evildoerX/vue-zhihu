<template>
  <div id="app">  
    <router-view></router-view>
    <!-- <img @click="inToLogin" src="./assets/logo.png">
    <hello></hello> --> 
  </div>
</template>

<script>
import "normalize.css" 
import "./scss/_container.scss"  

// import Hello from './components/Hello'

export default {
  // name: 'app',
  data () {
    return { 
    }
  },
  created () {  
  },
  components: {
    // Hello, 
  }, 
  watch: {
      '$route'(to, from) {//监听路由改变
          let user = sessionStorage.getItem('accessToken') ;
          if (!user) {
            this.$router.push('/login')
          } 
      }
  },
  methods: {
    inToLogin: function() {
      var vm = this;
      // 触发路由跳转
      // vm.$router.push({name:'login'});
    }
  }
}
</script>

<style lang="scss">
  @import "../node_modules/font-awesome/css/font-awesome.min.css";
  html,body{
    height: 100%;
  }
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale; 
    color: #2c3e50;  
    background: #435571;
    min-height: 100%; 
    .loading-container{
      text-align: center;
    }
  }
</style>
