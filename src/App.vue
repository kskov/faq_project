<template>
  <div id="app">
    <h1>FAQs</h1>
    <hr>
    <QuestionsList />
  </div>
</template>

<script>
import QuestionsList from '@/components/QuestionsList'
export default {
  name: 'app',
  components: {
    QuestionsList
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
