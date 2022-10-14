<template>
  <div id="app">
    <AccountInfo2 msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import AccountInfo from './components/AccountInfo.vue'
import AccountInfo2 from './components/AccountInfo2.vue'

export default {
  name: 'App',
  components: {
    AccountInfo2
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}
</style>
