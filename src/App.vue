<template>
  <div id="app">
    <div class="left">
      <img alt="Vue logo" src="./assets/logo.png">
    </div>
    <drag-line :is-horizon="false" />
    <div class="right">
      <div class="rigth-top">
        right-top
      </div>
      <drag-line :is-horizon="true" />
      <div>
        right-bottom
      </div>
    </div>
  </div>
</template>

<script>
import DragLine from './components/DragLine.vue'

export default {
  name: 'App',
  components: {
    DragLine
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
  margin-top: 60px;
  display: flex;
  height: 100%;
}
.left {
  flex-basis: 300px;
  width: 0;
  display: felx;
  flex-direction: column;
}
.right {
  flex: 1;
  width: 0;
  display: flex;
  flex-direction: column;
}
.rigth-top {
  flex-basis: 300px;
  height: 0;
}
.right-bottom {
  flex: 1;
  height: 0;
}
</style>
