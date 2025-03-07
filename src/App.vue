<template>
  <HelloWorld msg="BMI Calculator"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
background: #FFE897;

background: linear-gradient(180deg, #FFE897 0%, #FFB49C 100%);

background: -moz-linear-gradient(180deg,  #FFE897 0%, #FFB49C 100%);

background: -webkit-linear-gradient(180deg,  #FFE897 0%, #FFB49C 100%);
height: 100%;
width: 100%;
}
</style>
