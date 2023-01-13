<template>
  <div id="app">
    <Game />
  </div>
</template>

<script>
import Game from "./components/Game.vue";

export default {
  name: "App",
  components: {
    Game,
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: #212934;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.invisible {
  opacity: 0;
}

.visible {
  opacity: 1;
}

.container-character {
  width: 100%;
  display: flex;
  justify-content: center;
}
</style>
