<template>
  <div id="app">
      <h1>Quiz App</h1>
      
        <quizApp />
     
    
  </div>
</template>

<script>
import quizApp from './components/quizApp.vue';

export default {
  name: 'App',
  components: {
    quizApp,
  }
}
</script>

<style scoped>
#app {
  color:whitesmoke;
  display: flex;
    height: 100vh;
    width: 100vw;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    flex-direction: column;
    align-items: center;

}


</style>
