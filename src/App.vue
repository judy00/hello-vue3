<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <div>
    <!-- <Conditions></Conditions> -->
    <DynamicComp></DynamicComp>
    <AsyncImport></AsyncImport>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import Conditions from './components/Conditions'
import DynamicComp from './components/dynamicComp/DynamicComp'
// import AsyncImport from './components/dynamicComp/AsyncImport'

export default {
  name: 'App',
  components: {
    // HelloWorld,
    // Conditions,
    DynamicComp,
    // AsyncImport
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
