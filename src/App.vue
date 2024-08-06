<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
import './assets/styles.css' 
export default {
  name: 'App'
};
</script>

<style>
/* Estilos globales para la aplicación */
body {
  font-family: 'Comic Sans MS', 'Comic Sans', cursive;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-color: #f5f5f5;
}

#app {
  text-align: center;
}

header {
  background-color: #ffcb05;
  padding: 20px;
  color: #2a75bb;
}

h1 {
  margin: 0;
}
</style>