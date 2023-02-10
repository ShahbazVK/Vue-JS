<template>
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <HomeComponent/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import HomeComponent from './components/HomeComponent.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    HomeComponent,
  }
}
</script>