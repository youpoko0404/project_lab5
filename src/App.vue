<template>
<body>
  <div id="app">
    <fight msg />
  </div>
</body>
</template>

<script>
import fight from "./components/fight.vue";

export default {
  name: "App",
  components: {
    fight,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased; 
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  padding: 3em;
}
body {
  background-image: url("./assets/img/5311.jpg");
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
