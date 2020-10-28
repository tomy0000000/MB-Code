<template>
  <div class="verticle-middle">
    <CodeHeader msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import CodeHeader from "./components/CodeHeader.vue";

export default {
  name: "App",
  components: {
    CodeHeader,
  },
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: table;
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
}

.verticle-middle {
  display: table-cell;
  vertical-align: middle;
}
</style>
