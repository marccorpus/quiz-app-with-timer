<template>
  <div id="app">
    <QuizApp />
  </div>
</template>

<script>
import QuizApp from "./components/QuizApp.vue";

export default {
  components: {
    QuizApp,
  },
};
</script>

<style>
body {
  background-color: #2c62ef !important;
}
#app {
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-bottom: 20px;
}
</style>
