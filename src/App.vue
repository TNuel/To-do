<template>
  <div class="header">
    <h1>{{ title }}</h1>
    <p>Welcome to a well planned life (*_*)</p>
  </div>

  <Form />
</template>

<script>
import Form from './components/Form.vue'

export default {
  name: 'App',
  components: { Form },
  data() {
    return {
      title: 'My To-Do List :)',
      
    }
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
  margin: 40px;
  background-color: aqua;
  border-radius: 20px;
  height: 80vh;
}
@media screen and (max-width: 768px) {
  #app {
    background-color: aqua;
    max-width: 100%;
    height: 100vh;
    border-radius: 0;
    margin: 0;

  }
  h1 {
    font-size: 20px;
    padding: 20px;
  }
  /* .header {

  } */
}
</style>
