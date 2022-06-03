<template>
<!--  <img alt="Vue logo" src="./assets/logo.png">-->
<!--  <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  <div class="content">
    <div class="first-component">
      <GJAvgTickerValues></GJAvgTickerValues>
    </div>
    <div class="second-component">
      <GJButtons></GJButtons>
    </div>
  </div>

</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import GJAvgTickerValues from "@/components/GJAvgTickerValues";
import GJButtons from "@/components/GJButtons";

export default {
  name: 'App',
  components: {
    GJButtons,
    GJAvgTickerValues
    // HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.content{
  display: flex;
  flex-direction: row;
}
.first-component{
  min-width: 30%;
  max-width: 50%;
}
.second-component{
  display: flex;
  flex-direction: column;
}
</style>
