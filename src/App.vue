<template>
  <div id="app">
    <UserForm msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import UserForm from './components/userForm.vue'

export default {
  name: 'App',
  components: {
    UserForm
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

#app {
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 30px 0;
}
</style>
