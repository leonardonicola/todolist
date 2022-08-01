<template>
  <div id="app">
    <TodoList/>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoList
  }
}
</script>

<style>
*{
  box-sizing: border-box;
}

body,html{
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #004872;
  background-image: linear-gradient(
  40deg,
  hsl(0deg 0% 0%) 0%,
  hsl(0deg 0% 8%) 50%,
  hsl(0deg 0% 15%) 100%
);
  font-family: 'Helvetica';
}
#app {
  margin: 0;
  height: 100vh;
}
</style>
