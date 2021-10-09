<template>
  <div id="app container">
    <Admin />
  </div>
</template>

<script>
import Admin from "./components/Admin.vue";

export default {
  name: "App",
  components: {
    Admin,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.body {
  height: 100vh;
  width: 100vw;
}

.admin {
  position: relative;
}

.admin-modal {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
