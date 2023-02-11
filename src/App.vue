<template>
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <HomeComponent fruit="APPLE"/>
  <CourseGoals/>
  <MonsterSlayer/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import HomeComponent from './components/HomeComponent.vue'
import CourseGoals from './components/CourseGoals.vue'
import MonsterSlayer from './components/MonsterSlayer.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    HomeComponent,
    MonsterSlayer,
    CourseGoals,
  }
}
</script>