<template>
<body>
  <div id="app">
    <fight msg />
    <div class="row">
      <div class="col-3">
      </div>
    </div>
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
  color: #2c3e50;
}
body {
  background-image: url(./assets/img/bg.jpg);
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}
</style>
